
## AtliQ Grands hospitality Project


### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiMzhiYjI0YTctN2FmNC00NGZiLThhYjQtMGY0YjY2MThiNDU0IiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9

## Problem Statement

AtliQ Grands have been in the hospitality industry for the past 20 years . They are losing their market share and revenue in luxury/Business hotels category because of its ineffective decision making  to counter the strategic moves by its competitiors . This comprehensive dashboard helps the AtliQ Grands  to identify the areas they need  to increase their market share and revenue.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Loaded data into power Query for transforming the data.
- Step 3 : Promoted first row as headers for dim_rooms table.
- Step 4 : Data modeling was done by connecting all the dimension tables and fact tables by star schema.
- Step 5 : According to the AtliQ Grands they consider weekend as friday and saturday. So we created a seperate column in the dim_date table for the day_type to consider friday and saturday as weekends by using DAX measure.
 day_type = 
VAR wkd = WEEKDAY(dim_date[date])
RETURN
IF(wkd>5,"Weekend","Weekday")

- Step 6 : Created key metrics 
    
    1.Revenue

    2.RevPar = Total revenue / Total rooms available to sell

    Revpar = DIVIDE([Revenue],[Total Capacity],0)
    
    3.Occupancy% = Total rooms occupied/Total rooms available
    Occupancy % = DIVIDE([total succesfull bookings],[Total Capacity],0)
    
    4.ADR (Average Daily Rate)= Total rooms revenue/No of rooms   sold = ADR = DIVIDE( [Revenue], [Total Bookings],0)

    
    5.DSRN(Daily selling room over night) = DSRN = DIVIDE([Total Capacity], [No of days])


    6.Realisation = URN/BRN

    URN = Utilized room nights(i.e when customer stayed in room)

    BRN = Booked room night = URN+ No show + Cancellations

    7.Total Bookings =Total Bookings = COUNT(fact_bookings[booking_id])

    8.Total Capacity =Total Capacity = SUM(fact_aggregated_bookings[capacity])
    
    9.Total Succesful Bookings = Total Succesful Bookings = SUM(fact_aggregated_bookings[successful_bookings])
   
    10.Average Rating = Average Rating = AVERAGE(fact_bookings[ratings_given])
  
    11.No of days = No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1

    12.Total cancelled bookings = Total cancelled bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="Cancelled")

    13.Cancellation % = Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])

    14.Total Checked Out = Total Checked Out = CALCULATE([Total Bookings],fact_bookings[booking_status]="Checked Out")

    15.Total no show bookings  =  Total no show bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="No Show")

    16.No Show rate % = No Show rate % = DIVIDE([Total no show bookings],[Total Bookings])

    17.DURN (Daily Utilized Room Nights) = DURN = DIVIDE([Total Checked Out],[No of days])


    18.Revenue wow% = "To get the revenue change percentage week over week.Here, revcw  for current week,revpw for previous week ="Revenue WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"



- Step 7 : Similarly we calcuated wow% for Occupancy,ADR,revpar, realisation,DSRN 
    
- Step 8.  created card visualisation for key metrics by comparing with wow% (week over week change percentage).

- Step 9.  created line chart for key metrics trend over week number and day type.
- Step 10.  created visualisation for key metrics for different property, day type.

### Conclusion
 
 This dashboard developed for AtliQ Grands offers a comprehensive analysis of their performance in the luxury/business hotel category. This dashboard highlights key areas where AtliQ Grands is losing market share and revenue, providing actionable insights to address their current challenges. By  identifying underperforming segments, the dashboard enables the decision-makers at AtliQ Grands to take proactive steps towards enhancing their market position.
   
