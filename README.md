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

### **Uninstall Conflicting Versions**  

If you already have **DJITelloPy** installed, it's recommended to **uninstall it first** to avoid conflicts, as both libraries share the same name. Run one of the following commands:

```sh
pip uninstall djitellopy
```
or  
```sh
pip3 uninstall djitellopy  # Replace 'pip3' with the version you used to install djitellopy
```

---

## **Differences from the Original DJITelloPy**  
For the following examples, the code was setup like this
```python
from djitellopy import Tello  
from time import sleep # use sleep()

# Initialize the drone  
drone = Tello(retry_count=4)  

# Connect to the drone without retrying connection failures  
drone.connect(False)  

# Wait 1 second to ensure a stable connection  
sleep(1)  
```

### **Enhanced Takeoff**  

```python
drone.takeoff(battery_threshold=False)
```
- If `battery_threshold=False`, the drone will **take off without checking battery levels**.  
- If a value is provided (e.g., `drone.takeoff(30)`), the drone will **check its battery level before takeoff**. If the battery is below the threshold, it **will not** take off.  
- If left blank, the **default threshold (20%)** is used.  

---

### **Keep-Alive Functionality**  

```python
drone.keepalive(mode, param)
```
This command **prevents the drone from landing** after 7-10 seconds of inactivity by keeping the connection active.  

#### **Usage Modes:**  

1. **Automatic Mode (`mode="auto"`)**  
   - By default, this mode **sends keep-alive signals until the Enter key is pressed**.  
   ```python
   drone.keepalive("auto")
   ```
   - If a **user prompt** is needed, provide a `param` argument (a string for the prompt message).  
   ```python
   result = drone.keepalive("auto", "Enter a response:")  
   print(result)  # Returns the user input
   ```
  
2. **Timed Mode (`mode="time"`)**  
   - Requires `param` to be a **float or integer**, specifying the duration (in seconds) to send the keep-alive command.  
   ```python
   drone.keepalive("time", 5)   # Sends keep-alive for 5 seconds  
   drone.keepalive("time", 0.5) # Sends keep-alive for 0.5 seconds  
   ```

3. **Manual Start (`mode="start"`)**  
   - Starts continuously sending the keep-alive signal.  
   ```python
   drone.keepalive("start")  
   ```

4. **Manual Stop (`mode="stop"`)**  
   - Stops the keep-alive signal.  
   ```python
   drone.keepalive("stop")  
   ```

---

## **Documentation**  

For additional commands and usage, refer to the official **DJITelloPy** [documentation](https://djitellopy.readthedocs.io/en/latest/tello).  

---

## **License**  

This project follows the same **license** as DJITelloPy.  