# SQL-Experience

Created a Database for Pleasantville Community Theater Group 

Step 10.1 – Write out the normalized set of relations developed in Chapter 6 as the global schema.
    1. Zip(zip, city, state) 
    2. Production(perfDate, seasonStartDate, seasonEndDate, title) 
    3. Sponsor(sponsorID, firstName, lastName, street, zip, areaCode, phoneNumber) 
    4. Play(title, author, numberOfActs, setChanges)
    5. Member(memberID, dateJoined, lastName, firstName, street, zip, areaCode, phoneNumber, currentOfficeHeld) 
    6. DuesPayment(duesYear, memberID, amount, datePaid) 
    7. MemberProduction(memberID, year, seasonStartDate, role, task) 
    8. Performance(perfDate, year, time, seasonStartDate) 
    9. Subscriber(subID, firstName, lastName, street, zip, areaCode, phoneNumber ) 
    10. TicketSale(saleID, saleDate, totalAmount, perfDate, perfYear, subID, type) 
    11. Ticket(saleID, seatLocation, perfDate, type)  
    12. Types(type, price) 
    13. Donation(sponsorID, donationDate, donationType, donationValue, year, seasonStartDate) 
    
Step 10.2 - Write out a set of end user locations and the applications performed at each. Provide a reason to justify why you chose this data distribution plan.
The four locations are Pleasantville Community Theater Group Office (Main Site), Pleasantville Recreation Center, Clarkstown Highschool Theater Liaison Office and the Clarkstown High School South Auditorium Ticket Booth. 
The applications performed at each location EXCEPT Pleasantville Recreation Center are:
    1. Maintaining Ticket Sale records 
    2. Maintaining Ticket records 
    3. Maintaining Subscriber records
The applications performed at each location EXCEPT Pleasantville Recreation Center and Clarkstown High School South Auditorium Ticket Booth  are:
    4. Producing Admission Tickets
Applications that are performed at Pleasantville Community Group Office (Main site) and Pleasantville Recreation Center and Clarkstown Highschool Theater Liaison Office only are: 
    5. Producing the Production Details Report 
    6. Producing the Play Listings Report
    7. Producing the Performance Show report 
    8. Producing the Program - Cast and Credits report
    9. Producing Ticket Sale Reports
    10. Producing Program - Sponsors report
    11. Producing Subscriber Report
    12. Maintaining Production records
    13. Maintaining Play Listing Records
    14. Maintaining Member records
    15. Maintaining Dues Payment records
    16. Maintaining Ticket Type records
    17. Maintaining Sponsor records
    18. Producing Member report
    19. Producing Dues Payment Report
    20. Producing Donation Summary Report
    21. Producing Income Summary Report
    
Step 10.3 - For each application, decide what tables are required. 
    1. Producing the Admission Ticket - TicketSale, Ticket, Types, Performance and Production tables
    2. Producing the Ticket Sale Report - TicketSale, Ticket, Types, Performance and Production tables
    3. Maintaining the Ticket Sale records - TicketSale, Ticket, Types Table 
    4. Maintaining the Ticket records - Ticket, Types table
    5. Maintaining the Subscriber records - Subscriber, Zip Tables
    6. Producing the Production Details Report - Production, Performance, Play Tables 
    7. Producing the Play Listings Report - Play Table
    8. Producing the Performance Show report - Performance and Production Tables
    9. Producing the Program (Cast and Credits report) - Production, Member, Member-Production Tables
    10. Producing Program (Sponsors report) - Sponsor Table
    11. Producing Subscriber Report - Subscriber, Zip Tables
    12. Maintaining the Production records - Production Table
    13. Maintaining Play Listing Records - Play Table
    14. Maintaining the Member records - Member, Zip Tables
    15. Maintaining Dues Payment records - Member, DuesPayment Tables
    16. Producing the Member Report - Member, Zip Tables 
    17. Maintaining the Sponsor records - Sponsor, Zip Tables
    18. Maintaining Ticket Type records - Types Table
    19. Producing the Dues Payment Report - Member, DuesPayment Tables 
    20. Producing the Donation Summary Report - Donation, Sponsor Tables
    21. Producing the Income Summary Report - TicketSale, DuesPayment, Donation Tables

Step 10.4 - Using the normalized relations, perform selection and projection operations, to create the set of vertical, horizontal and mixed data fragments needed for each application.

Zip(zip, city, state) 
Since the table is rarely updated and is needed at every location, we will replicate the entire table at each branch.

Production(perfDate, seasonStartDate, seasonEndDate, title) .
The Production table record are used at # 1, 2, 6, 8, 9, 12 applications.
(1)and (2) use only part of the table, we will create a fragment for these apps:
ProductionFragment1= ΠperfDate, seasonStartDate,title (Production)

Sponsor(sponsorID, firstName, lastName, street, zip, areaCode, phoneNumber) 
Sponsor table records are used at (10), (17) and (20) apps and at 3 locations:
    Pleasantville Community Theater Group Office
    Clarkstown Highschool Theater Liaison Office
    Pleasantville Recreation Center

Each location will have its own Sponsor records.
SponsorPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Sponsor)
SponsorPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Sponsor)
SponsorClarkstownLiaison = σbranch=’ClarkstownLiaison’(Sponsor)

Play(title, author, numberOfActs, setChanges)
(7) and (13) use only title.
PlayTitleFragm = Πtitle(Play)

Member(memberID, dateJoined, lastName, firstName, street, zip, areaCode, phoneNumber, currentOfficeHeld) 
Fragment for 9, 15, 16, 19  apps:
MemberFragment1= ΠmemberID, lastName, firstName, currentOfficeHeld(Member)

DuesPayment(duesYear, memberID, amount, datePaid)
DuesPayment table records are used at 3 locations:
    Pleasantville Community Theater Group Office
    Clarkstown Highschool Theater Liaison Office
    Pleasantville Recreation Center

Each location will have its own DuesPayment records.
DuesPaymentPleasantvilleOffice = σbranch=’PleasantvilleOffice’(DuesPayment)
DuesPaymentPleasantvilleCenter = σbranch=’PleasantvilleCenter’(DuesPayment)
DuesPaymentClarkstownLiaison = σbranch=’ClarkstownLiaison’(DuesPayment)

MemberProduction(memberID, year, seasonStartDate, role, task)
 (9) uses  MemberProduction record at 3 locations we will replicate the entire table at each of these branch.

Performance(perfDate, year, time, seasonStartDate) 
Fragment for 1, 2, 8  app:
PerformanceFragment1= ΠperfDate, year(Performance)
Fragment for 6  app:
PerformanceFragment2= ΠperfDate, year, time(Performance)

Subscriber(subID, firstName, lastName, street, zip, areaCode, phoneNumber ) 
SubscriberPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Subscriber)
SubscriberPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Subscriber)
SubscriberClarkstownLiaison = σbranch=’ClarkstownLiaison’(Subscriber)
SubscriberClarkstownTicketB = σbranch=’ClarkstownTicketB’(Subscriber)

TicketSale(saleID, saleDate, totalAmount, perfDate, perfYear, subID, type) 
Fragment for (1):
TicketSaleFragment1= ΠsaleID, perfDate, type(TicketSale)
Fragment for (2) and (3):
TicketSaleFragment2= ΠsaleID,saleDate, totalAmount, perfDate, perfYear, subID, type(TicketSale)
Fragment for (4):
TicketSaleFragment3= ΠsaleID, totalAmount, perfYear, type(TicketSale)

Ticket(saleID, seatLocation, perfDate, type) 
TicketPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Ticket)
TicketPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Ticket)
TicketClarkstownLiaison = σbranch=’ClarkstownLiaison’(Ticket)
TicketClarkstownTicketB = σbranch=’ClarkstownTicketB’(Ticket)

Types(type, price) 
Since the table is rarely updated and is needed at every location, we will replicate the entire table at each branch.

Donation(sponsorID, donationDate, donationType, donationValue, year, seasonStartDate) 
Donations are associated with Sponsor. 
Pleasantville main site, Pleasantville Center and Clarkstown Liaison office will have its own Donation records.
DonationPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Donation)
DonationPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Donation)
DonationClarkstownLiaison = σbranch=’ClarkstownLiaison’(Donation)

Step 10.5 - Map the fragments to the applications and locations. 
For each fragment that is required at more than one application location, decide whether the fragment can be replicated, by considering frequency of use and of update.

Zip - This table is needed at every location, is rarely updated, and does not contain any sensitive date, so we replicate it everywhere. 
Production - This table would be updated infrequently due to productions updating only during a new season. The recreational center requires the attributes of this table, meaning it can be replicated at that branch. The liaison office and auditorium require a fragment called ProductionFragment1. The main table for production will be stored at the theater group’s main office.
Sponsor- This table will be updated more frequently than tables that are regularly updated infrequently, it would be infrequent enough to warrant replicating it. The theater group’s main office, liaison office and recreation center will have their own records of this table.
Play- This table would be updated at an infrequent basis since new plays would only be added/brought up at a new season.
Member- This table would be updated infrequently, assuming that new members join at an inconsistent period of time. We will have a MemberFragment1 that will be stored at 
DuesPayment- This table will be used/fragmented at the main office, liaison office and recreation center.
MemberProduction- This table will not be used frequently and it will be replicated at the recreational center branch.
Performance- This table will be updated infrequently. It will have two fragments, PerformanceFragment1 and PerformanceFragment2. 
Subscriber- This table will be updated frequently and every location will have remote access to this.
TicketSale- This table will be updated. Multiple fragments are present for this table, TicketSaleFragment1, TicketSaleFragment2, and TicketSaleFragment3.
Ticket- This table cannot be replicated at multiple locations due to preventing redundancy with values in the TicketSale table. The ticket table will be stored in the theater group’s main office.
Types-This table is needed at every location, is rarely updated, and does not contain any sensitive data, so we replicate it everywhere. 
Donation- This table is updated infrequently due to how often donations come to the theater group. The main office, liaison office and recreation center will have their own records and branches.
