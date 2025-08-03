
# Real-Time Trip Event Analysis

### name: Maryam Khalaf

##  Project Description
This project implements a real-time event-driven system for monitoring taxi trips. It uses **Azure Event Hub** for ingesting trip events, **Azure Function App** to analyze trip data, and a **Logic App** to process and post alerts to **Microsoft Teams** using Adaptive Cards.

---

##  Architecture

<img width="1580" height="980" alt="output" src="https://github.com/user-attachments/assets/a97001f0-5521-4357-a480-427b14a47add" />


**Flow:**
1. **Event Hub** ingests trip events in JSON format.
2. **Function App (`analyze_trip`)** analyzes each trip to detect:
   - Long trips
   - Group rides (passengers > 4)
   - Cash payments
   - Suspicious vendor activity (cash + very short trips)
3. **Logic App** processes results:
   - If `isInteresting = true`, posts "Interesting Trip Detected" card.
   - If insights include `SuspiciousVendorActivity`, posts a "Suspicious Vendor Activity" card.
   - Otherwise, posts "Trip Analyzed – No Issues" card.
4. Alerts are sent to **Microsoft Teams**.

---

##  Steps Followed
 1- Created an **Event Hub** and sent trip events in JSON format.  
 2- Built an **Azure Function App (`analyze_trip`)** to analyze trips.  
 3- Designed a **Logic App** with:
   - For Each loop over the function output
   - Conditions for `isInteresting` and `SuspiciousVendorActivity`
   - Adaptive Cards posting results to Teams  
 4- Connected Logic App to **Microsoft Teams**.

---

##  Example JSON Inputs
###  Normal Trip
```json
{
    "vendorID": "3",
    "tripDistance": 3.02,
    "passengerCount": 2,
    "paymentType": 3
}
```

###  Suspicious Trip
```json
{
    "vendorID": "V004",
    "tripDistance": 0.5,
    "passengerCount": 2,
    "paymentType": 2
}
```

---

##  Example Outputs
### Normal Trip (Teams Card)
-  Trip Analyzed – No Issues  
- Vendor: 3  
- Distance: 3.02 mi  
- Passengers: 2  
- Payment: 3  
- Summary: Trip normal  

### Suspicious Trip (Teams Card)
-  Interesting Trip Detected  
- Vendor: V004  
- Distance: 0.5 mi  
- Passengers: 2  
- Payment: 2  
- Insights: CashPayment, SuspiciousVendorActivity  

---

##  Demo Video

https://youtu.be/wWK2SRh8ojk


---
