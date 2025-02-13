# DJITelloPy-UCAS  

**DJITelloPy-UCAS** is a modified version of [DJITelloPy](https://github.com/damiafuentes/DJITelloPy), adding enhanced functionality for **takeoff** and **keep-alive mechanisms**.  

## Installation  

Clone the repository and install dependencies:  
```sh
git clone https://github.com/jaguarclaws2007/DJITelloPy-UCAS.git
cd DJITelloPy-UCAS
pip install -r requirements.txt
```  

Or install directly via pip:  
```sh
pip install git+https://github.com/jaguarclaws2007/DJITelloPy-UCAS.git
```  
---

If you want to uninstall DJITellopy to **free up** space, you can run: 

```sh
pip uninstall djitellopy
```
or  
```sh
pip3 uninstall djitellopy  # Replace 'pip3' with the version you used to install djitellopy
```

---

## **Differences from the Original DJITelloPy**  

### **Setup**  
Before running the following examples, ensure your drone is set up like this:  

```python
from tellopy import Tello
from time import sleep  

# Initialize the drone  
drone = Tello(retry_count=4)  

# Connect to the drone without retrying failed connections  
drone.connect(False)  

# Wait 1 second to ensure a stable connection  
sleep(1)  
```

---

### **Enhanced Takeoff**  
```python
drone.takeoff(battery_threshold=20)
```
- If `battery_threshold=False`, the drone will **take off without checking battery levels**.  
- If a value is provided (e.g., `drone.takeoff(30)`), the drone will **check its battery level before takeoff**.  
  - If the battery is **below** the threshold, it **will not** take off.  
- If left blank, the **default threshold (20%)** is used.  
- Ex:
   ```python
   drone.takeoff() # will defualt to a battery threshold of 20%
   drone.takeoff(False) # will take off without checking battery levels
   drone.takeoff(25) # will set the threshold to 25% (can be a number 1-100)
   ```

---

### **Keep Alive**  
```python
drone.keep_alive(mode, param=None)
```
This function keeps the connection to the drone alive, preventing it from landing after 7-10 seconds of inactivity.  

#### **Usage Modes:**  

1. **Automatic Mode (`mode="auto"`)**  
   - By default, this mode sends keep-alive signals until the **Enter key** is pressed.  
   ```python
   drone.keep_alive("auto")
   drone.keep_alive() # Can also be ran this way as auto is the defualt mode.
   ```
   - If a **user prompt** is needed, provide `param` as a question string:  
   ```python
   result = drone.keep_alive("auto", "Enter a response:")  
   print(result)  # Returns the user input
   ```

2. **Timed Mode (`mode="time"`)**  
   - Requires `param` to be a **float or integer** (seconds to keep alive).  
   ```python
   drone.keep_alive("time", 5)   # Sends keep-alive for 5 seconds  
   drone.keep_alive("time", 0.5) # Sends keep-alive for 0.5 seconds  
   ```

3. **Manual Start (`mode="start"`)**  
   - Starts continuously sending the keep-alive signal.  
   ```python
   drone.keep_alive("start")  
   ```

4. **Manual Stop (`mode="stop"`)**  
   - Stops the keep-alive signal.  
   ```python
   drone.keep_alive("stop")  
   ```

---

## **Documentation**  

For additional commands and usage, refer to the official **DJITelloPy** [documentation](https://djitellopy.readthedocs.io/en/latest/tello).  

---

## **License**  

This project follows the same **license** as DJITelloPy.  
