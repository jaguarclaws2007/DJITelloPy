# DJITelloPy-UCAS  

DJITelloPy-UCAS is a modified version of [DJITelloPy](https://github.com/damiafuentes/DJITelloPy), adding enhanced functionality for takeoff and keep-alive mechanisms.  

## Installation  

Clone the repository and install dependencies:
`git clone https://github.com/jaguarclaws2007/DJITelloPy-UCAS.git
cd DJITelloPy-UCAS
pip install -r requirements.txt`

Or install directly via pip:
`pip install git+https://github.com/jaguarclaws2007/DJITelloPy-UCAS.git `

## Differences from the Original DJITelloPy

### Takeoff

drone.takeoff(battery_threshold=False)

If battery_threshold is False, the drone will take off without checking battery levels.

If a value is provided (e.g., drone.takeoff(30)), the drone will check its battery level before taking off. If the battery is below the threshold, it will not take off.

If left blank, the default threshold (20%) is used.


### Keep Alive

There are two ways to maintain the connection to the drone: automatic and manual.

#### Automatic Keep-Alive

drone.keepalive()

This method starts the keep-alive process and waits for the user to press Enter.

Once Enter is pressed, the keep-alive process stops.


#### Manual Keep-Alive

drone.start_keepalive()  # Start keep-alive
drone.stop_keepalive()   # Stop keep-alive

start_keepalive() begins sending keep-alive packets.

stop_keepalive() stops the keep-alive process.


## Documentation

For additional commands and usage, refer to the original DJITelloPy documentation.

## License

This project follows the same license as DJITelloPy.


