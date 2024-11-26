# Deep Dive: Streaks

## Streak Scenario's

**+**  = New Ride  
**|** = Existing Ride  
**△** = Streak  

### **+**   (Isolated Single Ride)
**Description**:  
No streak exists. The new ride is a single isolated ride with no other rides the day before or after.  
**Action**:  
No streak is created. The ride remains a single, standalone activity.

---

### **|****+** (New Two-Ride Streak)
**Description**:  
The new ride directly follows an existing single ride (X), forming a two-ride streak.  
**Action**:  
Create a new streak combining the single ride and the new ride.

---

### **+** **|** (Out-of-Order Two-Ride Streak Creation)
**Description**:  
The new ride is the day before an existing single ride, forming a two-ride streak.  
**Action**:  
Create a new streak combining the new ride and the existing single ride.

---

### **|** **+** **|** (Three-Ride Streak Creation)
**Description**:  
The new ride bridges two existing single rides, forming a streak of three rides.  
**Action**:  
Create a new streak combining all three rides.

---

### **△** **+** (Extend an Existing Streak)
**Description**:  
The new ride directly follows the last ride of an existing streak, extending the streak.  
**Action**:  
Update the streak’s end date and length to include the new ride.

---

### **+** **△** (Pad an Existing Streak)
**Description**:  
The new ride is added before the start of an existing streak, extending the streak backward.  
**Action**:  
Update the streak’s start date and length to include the new ride.

---

### **△** **+** **△** (Merge Two Streaks)
**Description**:  
The new ride falls between two existing streaks, bridging them into a single streak.  
**Action**:  
Merge the two streaks and the new ride into one continuous streak.