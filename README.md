# SQL-Experience

Created a Database for Pleasantville Community Theater Group 

Read the sample project steps for this chapter and apply the same techniques to the team project that you are developing. Use the normalized set of relations developed in Chapter 6 as the global schema. For the team project, assume that there are at least four locations or branches for the enterprise and that the processing is to be distributed to these locations. Identify the applications that will be performed at each of the locations and then follow the steps below to plan the distribution of your database. 

**Step 10.1 – Write out the normalized set of relations developed in Chapter 6 as the global schema.**

1. **Zip(**zip, city, state**)** 
1. **Production(***perfDate*, *seasonStartDate*, seasonEndDate, *title***)** 
1. **Sponsor(**sponsorID, firstName, lastName, street, *zip*, areaCode, phoneNumber**)** 
1. **Play(**title, author, numberOfActs, setChanges**)**
1. **Member(**memberID, dateJoined, lastName, firstName, street, *zip*, areaCode, phoneNumber, currentOfficeHeld**)** 
1. **DuesPayment(**duesYear, *memberID*, amount, datePaid**)** 
1. **MemberProduction(***memberID, year, seasonStartDate,* role, task**)** 
1. **Performance(**perfDate, *year*, time, *seasonStartDate***)** 
1. **Subscriber(**subID, firstName, lastName, street, *zip,* areaCode, phoneNumber **)** 
1. **TicketSale(**saleID, saleDate, totalAmount, *perfDate, perfYear, subID, type***)** 
1. **Ticket(***saleID*, seatLocation, *perfDate*, *type***)**  
1. **Types(**type, price**)** 
1. **Donation(***sponsorID*, donationDate, donationType, donationValue, *year, seasonStartDate***)** 



**Step 10.2 - Write out a set of end user locations and the applications performed at each. Provide a reason to justify why you chose this data distribution plan.**

The four locations are Pleasantville Community Theater Group Office (Main Site), Pleasantville Recreation Center, Clarkstown Highschool Theater Liaison Office and the Clarkstown High School South Auditorium Ticket Booth. 

The applications performed at each location EXCEPT Pleasantville Recreation Center are:

1. Maintaining Ticket Sale records 
1. Maintaining Ticket records 
1. Maintaining Subscriber records

The applications performed at each location EXCEPT Pleasantville Recreation Center and Clarkstown High School South Auditorium Ticket Booth  are:

1. Producing Admission Tickets

Applications that are performed at Pleasantville Community Group Office (Main site) and Pleasantville Recreation Center and Clarkstown Highschool Theater Liaison Office only are: 

1. Producing the Production Details Report 
1. Producing the Play Listings Report
1. Producing the Performance Show report 
1. Producing the Program - Cast and Credits report
1. Producing Ticket Sale Reports
1. Producing Program - Sponsors report
1. Producing Subscriber Report
1. Maintaining Production records
1. Maintaining Play Listing Records
1. Maintaining Member records
1. Maintaining Dues Payment records
1. Maintaining Ticket Type records
1. Maintaining Sponsor records
1. Producing Member report
1. Producing Dues Payment Report
1. Producing Donation Summary Report
1. Producing Income Summary Report

**Step 10.3 - For each application, decide what tables are required.** 

1. Producing the Admission Ticket - TicketSale, Ticket, Types, Performance and Production tables
1. Producing the Ticket Sale Report - TicketSale, Ticket, Types, Performance and Production tables
1. Maintaining the Ticket Sale records - TicketSale, Ticket, Types Table 
1. Maintaining the Ticket records - Ticket, Types table
1. Maintaining the Subscriber records - Subscriber, Zip Tables
1. Producing the Production Details Report - Production, Performance, Play Tables 
1. Producing the Play Listings Report - Play Table
1. Producing the Performance Show report - Performance and Production Tables
1. Producing the Program (Cast and Credits report) - Production, Member, Member-Production Tables
1. Producing Program (Sponsors report) - Sponsor Table
1. Producing Subscriber Report - Subscriber, Zip Tables
1. Maintaining the Production records - Production Table
1. Maintaining Play Listing Records - Play Table
1. Maintaining the Member records - Member, Zip Tables
1. Maintaining Dues Payment records - Member, DuesPayment Tables
1. Producing the Member Report - Member, Zip Tables 
1. Maintaining the Sponsor records - Sponsor, Zip Tables
1. Maintaining Ticket Type records - Types Table
1. Producing the Dues Payment Report - Member, DuesPayment Tables 
1. Producing the Donation Summary Report - Donation, Sponsor Tables
1. Producing the Income Summary Report - TicketSale, DuesPayment, Donation Tables

**Step 10.4 - Using the normalized relations, perform selection and projection operations, to create the set of vertical, horizontal and mixed data fragments needed for each application.**

**Zip(**zip, city, state**)** 

Since the table is rarely updated and is needed at every location, we will replicate the entire table at each branch.

**Production(***perfDate*, *seasonStartDate*, seasonEndDate, *title***) .**

The Production table record are used at # 1, 2, 6, 8, 9, 12 applications.

(1)and (2) use only part of the table, we will create a fragment for these apps:

ProductionFragment1= **Π**perfDate, seasonStartDate,title (Production)

**Sponsor(**sponsorID, firstName, lastName, street, *zip*, areaCode, phoneNumber**)** 

Sponsor table records are used at (10), (17) and (20) apps and at 3 locations:

- Pleasantville Community Theater Group Office
- Clarkstown Highschool Theater Liaison Office
- Pleasantville Recreation Center

Each location will have its own Sponsor records.

SponsorPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Sponsor)

SponsorPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Sponsor)

SponsorClarkstownLiaison = σbranch=’ClarkstownLiaison’(Sponsor)

**Play(**title, author, numberOfActs, setChanges**)**

(7) and (13) use only title.

PlayTitleFragm = **Π**title(Play)

**Member(**memberID, dateJoined, lastName, firstName, street, *zip*, areaCode, phoneNumber, currentOfficeHeld**)** 

Fragment for 9, 15, 16, 19  apps:

MemberFragment1= **Π**memberID, lastName, firstName, currentOfficeHeld(Member)

**DuesPayment(**duesYear, memberID, amount, datePaid**)**

DuesPayment table records are used at 3 locations:

- Pleasantville Community Theater Group Office
- Clarkstown Highschool Theater Liaison Office
- Pleasantville Recreation Center

Each location will have its own DuesPayment records.

DuesPaymentPleasantvilleOffice = σbranch=’PleasantvilleOffice’(DuesPayment)

DuesPaymentPleasantvilleCenter = σbranch=’PleasantvilleCenter’(DuesPayment)

DuesPaymentClarkstownLiaison = σbranch=’ClarkstownLiaison’(DuesPayment)

**MemberProduction(***memberID, year, seasonStartDate,* role, task**)**

` `(9) uses  MemberProduction record at 3 locations we will replicate the entire table at each of these branch.

**Performance(**perfDate, *year*, time, *seasonStartDate***)** 

Fragment for 1, 2, 8  app:

PerformanceFragment1= **Π**perfDate, year(Performance)

Fragment for 6  app:

PerformanceFragment2= **Π**perfDate, year, time(Performance)




**Subscriber(**subID, firstName, lastName, street, *zip,* areaCode, phoneNumber **)** 

SubscriberPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Subscriber)

SubscriberPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Subscriber)

SubscriberClarkstownLiaison = σbranch=’ClarkstownLiaison’(Subscriber)

SubscriberClarkstownTicketB = σbranch=’ClarkstownTicketB’(Subscriber)

**TicketSale(**saleID, saleDate, totalAmount, *perfDate, perfYear, subID, type***)** 

Fragment for (1):

TicketSaleFragment1= **Π**saleID, perfDate, type(TicketSale)

Fragment for (2) and (3):

TicketSaleFragment2= **Π**saleID,saleDate, totalAmount, perfDate, perfYear, subID, type(TicketSale)

Fragment for (4):

TicketSaleFragment3= **Π**saleID, totalAmount, perfYear, type(TicketSale)

**Ticket(***saleID*, seatLocation, *perfDate*, *type***)** 

TicketPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Ticket)

TicketPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Ticket)

TicketClarkstownLiaison = σbranch=’ClarkstownLiaison’(Ticket)

TicketClarkstownTicketB = σbranch=’ClarkstownTicketB’(Ticket)

**Types(**type, price**)** 

Since the table is rarely updated and is needed at every location, we will replicate the entire table at each branch.

**Donation(***sponsorID*, donationDate, donationType, donationValue, *year, seasonStartDate***)** 

Donations are associated with Sponsor. 

Pleasantville main site, Pleasantville Center and Clarkstown Liaison office will have its own Donation records.

DonationPleasantvilleOffice = σbranch=’PleasantvilleOffice’(Donation)

DonationPleasantvilleCenter = σbranch=’PleasantvilleCenter’(Donation)

DonationClarkstownLiaison = σbranch=’ClarkstownLiaison’(Donation)

**Step 10.5 - Map the fragments to the applications and locations.** 

For each fragment that is required at more than one application location, decide whether the fragment can be replicated, by considering frequency of use and of update.

**Zip -** This table is needed at every location, is rarely updated, and does not contain any sensitive date, so we replicate it everywhere. 

**Production -** This** table would be updated infrequently due to productions updating only during a new season. The recreational center requires the attributes of this table, meaning it can be replicated at that branch. The liaison office and auditorium require a fragment called ProductionFragment1. The main table for production will be stored at the theater group’s main office.

**Sponsor-** This table will be updated more frequently than tables that are regularly updated infrequently, it would be infrequent enough to warrant replicating it. The theater group’s main office, liaison office and recreation center will have their own records of this table.

**Play-** This table would be updated at an infrequent basis since new plays would only be added/brought up at a new season.

**Member-** This table would be updated infrequently, assuming that new members join at an inconsistent period of time. We will have a MemberFragment1 that will be stored at 

**DuesPayment-** This table will be used/fragmented at the main office, liaison office and recreation center.

**MemberProduction-** This table will not be used frequently and it will be replicated at the recreational center branch.

**Performance-** This table will be updated infrequently. It will have two fragments, PerformanceFragment1 and PerformanceFragment2. 

**Subscriber-** This table will be updated frequently and every location will have remote access to this.

**TicketSale-** This table will be updated. Multiple fragments are present for this table, TicketSaleFragment1, TicketSaleFragment2, and TicketSaleFragment3.

**Ticket-** This table cannot be replicated at multiple locations due to preventing redundancy with values in the TicketSale table. The ticket table will be stored in the theater group’s main office.

**Types-**This table is needed at every location, is rarely updated, and does not contain any sensitive data, so we replicate it everywhere. 

**Donation-** This table is updated infrequently due to how often donations come to the theater group. The main office, liaison office and recreation center will have their own records and branches.

**Step 10.6 - Make a table showing a geographical network, listing nodes and applications and showing the data fragments at each node.**

`	`**Shown In Figure 10.6**


|**Application** |**Main Site - Group Office** |**Recreational Center**|**Auditorium Ticket Booth**|**Liaison Office**|
| :- | :- | :- | :- | :- |
|1\. Producing the Admission Ticket |<p>TicketSaleFragment1</p><p>PerformanceFragment1</p><p>ProductionFragment1</p><p>TicketPleasantvilleOffice </p><p>Types</p>|||<p>TicketSaleFragment1</p><p>PerformanceFragment1</p><p>ProductionFragment1</p><p>TicketClarkstownLiaison </p><p>Types</p>|
|2\. Producing the Ticket Sale Report |<p>ProductionFragment1</p><p>PerformanceFragment1</p><p>TicketSaleFragment2</p><p>TicketPleasantvilleOffice </p><p>Types</p>|<p>ProductionFragment1</p><p>PerformanceFragment1</p><p>TicketSaleFragment2</p><p>TicketClarkstownLiaison </p><p>Types</p>||<p>ProductionFragment1</p><p>PerformanceFragment1</p><p>TicketSaleFragment2</p><p>TicketClarkstownLiaison </p><p>Types</p>|
|` `3. Maintaining the Ticket Sale records |<p>TicketSaleFragment2</p><p>TicketPleasantvilleOffice </p><p>Types</p>||<p>TicketSaleFragment2</p><p>TicketClarkstownTicketB</p><p>Types</p>|<p>TicketSaleFragment2</p><p>TicketClarkstownLiaison </p><p>Types</p>|
|4\. Maintaining the Ticket records|<p>TicketPleasantvilleOffice</p><p>Types</p>|<p></p><p></p>|<p>TicketClarkstownTicketB</p><p>Types</p><p></p>|<p>TicketClarkstownLiaison</p><p>Types</p><p></p>|
|5\. Maintaining the Subscriber records |<p>SubscriberPleasantvilleOffice  </p><p>Zip</p>||<p>SubscriberClarkstownTicketB</p><p>Zip</p>|<p>SubscriberClarkstownLiaison </p><p>Zip</p>|
|6\. Producing the Production Details Report |<p>Production</p><p>Play</p><p>PerformanceFragment2</p>||<p>Production</p><p>Play</p><p>PerformanceFragment2</p>|<p>Production</p><p>Play</p><p>PerformanceFragment2</p>|
|7\. Producing the Play Listings Report |PlayTitleFragm |PlayTitleFragm ||PlayTitleFragm |
|8\. Producing the Performance Show report|<p>Production</p><p>PerformanceFragment1</p>|<p>Production,</p><p>PerformanceFragment1</p>||<p>Production</p><p>PerformanceFragment1</p>|
|9\. Producing the Program (cast and credits report)|<p>Production</p><p>MemberFragment1</p><p>MemberProduction</p>|<p>Production</p><p>MemberFragment1</p><p>MemberProduction</p>||<p>Production</p><p>MemberFragment1</p><p>MemberProduction</p>|
|10\. Producing Program (Sponsors Report)|SponsorPleasantvilleOffice |SponsorPleasantvilleCenter ||SponsorClarkstownLiaison |
|11\. Producing Subscriber Report|<p>Zip</p><p>SubscriberPleasantvilleOffice </p>|<p>Zip</p><p>SubscriberPleasantvilleCenter</p>||<p>Zip</p><p>SubscriberClarkstownLiaison </p>|
|<p>12\. </p><p>Maintaining the Production records</p>|Production|Production||Production|
|<p>13\.</p><p>Maintaining Play Listing Records</p>|PlayTitleFragm |PlayTitleFragm ||PlayTitleFragm |
|<p>14\.</p><p>Maintaining  Member records</p>|<p>Member</p><p>` `Zip</p>|<p>Member</p><p>` `Zip</p>||<p>Member</p><p>` `Zip</p>|
|15\. Maintaining Dues Payment records|<p>MemberFragment1</p><p>DuesPaymentPleasantvilleOffice </p>|<p>MemberFragment1</p><p>DuesPaymentPleasantvilleCenter</p><p> </p>||<p>MemberFragment1</p><p>DuesPaymentClarkstownLiaison </p>|
|16\. Producing the Member report|<p>MemberFragment1</p><p>` `Zip</p>|<p>MemberFragment1</p><p>` `Zip</p>||<p>MemberFragment1</p><p>` `Zip</p>|
|17\. Maintaining sponsor records|<p>SponsorPleasantvilleOffice</p><p>Zip</p>|<p>SponsorPleasantvilleCenter</p><p>Zip</p>||<p>SponsorClarkstownLiaison </p><p>Zip</p>|
|18\. Maintaining Ticket Types records|Types|Types||Types|
|19\. Producing the Dues Payment Report|<p>MemberFragment1</p><p>DuesPaymentPleasantvilleOffice</p><p></p>|<p>MemberFragment1</p><p>DuesPaymentPleasantvilleCenter</p><p></p>||<p>MemberFragment1</p><p>DuesPaymentClarkstownLiaison </p><p></p>|
|20\. Producing Donation Summary Report |<p>SponsorPleasantvilleOffice</p><p>DonationPleasantvilleOffice </p>|<p>DonationPleasantvilleCenter</p><p>SponsorPleasantvilleCenter</p><p></p>||<p>DonationClarkstownLiaison </p><p>SponsorClarkstownLiaison</p>|
|21\. Producing Income Summary Report|<p>TicketSaleFragment3</p><p>DuesPaymentPleasantvilleOffice</p><p>DonationPleasantvilleOffice</p><p></p><p></p>|<p>TicketSaleFragment3</p><p>DuesPaymentPleasantvilleCenter</p><p>DonationPleasantvilleCenter</p>||<p>TicketSaleFragment3</p><p>DuesPaymentClarkstownLiaison</p><p>DonationClarkstownLiaison</p>|

**Figure 10.6- Geographical Network for The Pleasantville Community Theater Group**

**Step 10.7 - For each application in the geographical network, determine whether access will be local, remote, or compound.**

Make up a table showing each site, and the applications requiring local access, remote access, and compound access.


|**Application** |**Main Site - Group Office** |**Recreational Center**|**Auditorium Ticket Booth**|**Liaison Office**|
| :- | :- | :- | :- | :- |
|1\. Producing the Admission Ticket - all local access|local |local|local|local|
|2\. Producing the Ticket Sale Report - all local access|local |local|local|local|
|<p>` `3. Maintaining the Ticket Sale records -</p><p>remote access from center, auditorium and liaison office for subID, address, phone and name.</p>|local |remote|remote|remote|
|<p>4\. Maintaining the Ticket records - </p><p>all local access</p>|local |local|local|local|
|5\. Maintaining the Subscriber records - remote access from center, auditorium and liaison office for subID, address, phone and name.|local |remote|remote|remote|
|6\. Producing the Production Details Report - all local access|local |local|local|local|
|7\. Producing the Play Listings Report - all local access|local |local|local|local|
|8\. Producing the Performance Show report - all local access|local |local|local|local|
|9\. Producing the Program (cast and credits report) - all local access|local |local|local|local|
|10\. Producing Program (Sponsors Report) - all local access|local |local|local|local|
|11\. Producing Subscriber Report - all local access|local |local|local|local|
|<p>12\. </p><p>Maintaining the Production records - all local access</p>|local |local|local|local|
|<p>13\.</p><p>Maintaining Play Listing Records - all local access</p>|local |local|local|local|
|<p>14\.</p><p>Maintaining  Member records - all local access</p>|local |local|local|local|
|15\. Maintaining Dues Payment records - all local access|local |local|local|local|
|16\. Producing the Member report - all local access|local |local|local|local|
|17\. Maintaining sponsor records - all local access|local |local|local|local|
|18\. Maintaining Ticket Types records - all local access|local |local|local|local|
|19\. Producing the Dues Payment Report - all local access|local |local|local|local|
|20\. Producing Donation Summary Report - all local access|local |local|local|local|
|21\. Producing Income Summary Report - all local access|local |local|local|local|
**Figure 10.7- Applications with Local and Remote Access**

**Step 10.8 - For each of the non-local accesses, identify the application and the location of the data.** 

Estimate the number of accesses required per day using estimates such as low, medium, or high. If it is high, justify your choice of non-local storage. 

The only applications that would require remote access are Maintaining ticket sale records and Subscriber records, which will require that the other locations (auditorium booth, pleasantville center and liaison office access the Main site (Group Office) location to determine the subID, address, phone and name of the subscriber/buyer. This is done to avoid having overlapping tickets on record and booking tickets with different people in a group. The number of accesses would depend on how many tickets are being purchased at a time for each location that they are purchased. Other information for the theater group would only be accessed by those working administrative/managerial roles within the group for privacy/security purposes.

<a name="_heading=h.gjdgxs"></a>**Step 10.9 - Make any adjustments indicated by your analysis of applications and traffic, and plan a final geographical network.** 

<a name="_heading=h.qzc3p5pjx5yk"></a>Most accesses are local, there is no need to adjust the geographical network shown in Figure 10.7
