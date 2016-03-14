# OafInterview

##Dev Candidate Project: Seasonless Repayment 
###Overview
####Problem Description
Clients in our program purchase items each season on loan, and during the course of the season, they repay their credit. So clients have credit associated to them on a season by season basis. 

In our data model, we associated client’s repayments with a season where they have outstanding credit. These repayments are made either through cash payments to a field officer or through a mobile money platform (M-PESA). A member of our data input team will then take a record of all the repayments that clients have made and upload them to our application, which will then record each payment against the proper client in our database. 

When a client makes a payment, we need to know to which season that the debit will be applied, as there could exist times when clients have credit open in multiple seasons. Traditionally, we required that there be an associated repayment season with each payment that the client makes, so the application doesn’t have to make any decisions. To make it easier on clients, field officers, and other staff, we’re moving away from this model and dropping the requirement that seasons must be associated with each payment in the upload. Since we still require that repayments be linked with seasons in our database, we’re creating ‘pseudo-seasonless’ repayment logic that will determine which season the payment should be applied to. 

If a client makes a payment that will exceed the current remaining credit for a given season, then two repayment “adjustments” must be made. These adjustments are:
A negative adjustment associated with the season that was overpaid equal to the amount that the payment overpaid the credit.
A positive adjustment associated with the client’s next season equal to the amount that the payment overpaid the credit.
If, however, the client does not have outstanding credit in another season, then no adjustment will be made. 
####Deliverables
There are 2 deliverables for this project:
A service class that will accept a list of (RepaymentUploads) client repayments and will determine which season the repayment should be applied to. An updated repayment list should be output (Repayments) with the correct repayment amount and season for each repayment as well as a list of any repayment adjustments that must be made. 
A project post-mortem, outlining at least:
Current project status
Successes/what went well
Bumps/what you wished went better
How you would improve these things in future projects
Estimate on the outstanding work
Improvements/enhancements for future consideration
####Additional Considerations
You will be provided with sample data.  

You may use whatever development environment/language/framework you feel comfortable with.

You will be working with at least one member of the Dev team every day for a couple of hours, pair-programming the solution.  You will be driving.

This interview is designed to assess:
Your communication and critical-thinking style
Your problem-solving skills and strategies
Your ability to collaborate, when appropriate
Your ability to make and execute a project plan

This is not primarily a coding test, though the quality of your code will have some relationship to the success of the pair coding time.  Your coding skills are peripheral at this point.  You do NOT have to present a completed project, but you will be expected to present a post mortem on what went well and what you would have changed, in hindsight, as well as an estimate of how much work remains to be done and possible ‘stretch goals’ for the project


###Data Schema
####Seasons
SeasonID (int)
SeasonName (string)
StartDate (date)
EndDate (date)
####Customers
CustomerID (int)
CustomerName (string)
####CustomerSummaries
CustomerID (int)
SeasonID (int)
Credit (dec)
TotalRepaid (dec)
####RepaymentUploads
CustomerID (int)
SeasonID [optional] (int)
Date (date)
Amount (dec)
RepaymentID (int)
####Repayments (OUTPUT)
CustomerID (int)
SeasonID (int)
Date (date)
Amount (dec)
RepaymentID (int)
ParentID (int)

