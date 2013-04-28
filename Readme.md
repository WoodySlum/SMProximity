**SMProximity**

SMProximity is a small tool written in php which detect devices over Wifi and Bluetooth.
I use it with my RaspBerry Pi to enable specific actions when I go back / leave home such as put the light on.

The script first detects Wifi devices ; if not found it will try to scan the bluetooth devices.

**How to install**

Really easy :
First install arp-scan and, l2ping and bluetooth packages. Nohup is for running in background

`sudo apt-get install arp-scan`

`sudo apt-get install l2ping`

`sudo apt-get install bluetooth`

`sudo apt-get install nohup`

Copy the following PHP Class into logging.php : http://www.redips.net/php/write-to-log-file/

**How to configure**

Change the following part the code :

	// Config

	// Devices list
	var $devicesWifi = array(
		array("title" => "iPhone de Seb",
		      "mac" => "68:09:27:cd:37:d3")
	);

	var $devicesBt = array(
		array("title" => "iPhone de Seb",
		      "mac" => "68:09:27:CD:37:D4")
	);

	var $interface = "eth0"; // Network interface to scan
	var $wifiNetwork = "192.168.0.0/24"; // Network IP pattern to scan
	var $pause = 7; // Wait after scan. Means more Scan over X seconds
	var $maxAttempt = 8; // When detection failed, how many attempt before triggering the script
	var $logPath = "/var/log/proximity.log"; // The log file

Write your own instructions when device is detected or not :

	function detectionOk() {
		// Do your stuff when detection is Ok

		$this->msg("Found device");
	}
-

	function detectionKo() {
		// Do your stuff when detection is NOT Ok

		$this->msg("Oops device not found");
	}
	
Then make it executable

`chmod +x SMProximity`

**How to start**

Ok so just run the following command :

`nohup php SMProximity &`

