D365FO Smartbridge connector also includes a telemetry monitoring of the synchronizations performed through the connector, tracking minimal request data (time, sender, etc.).  
This functionality can be extended also for error diagnostic if necessary. In this case, the user must:
* First enable the standard D365FO feature **Monitoring and Telemetry** in D365FO Feature management when it is not enabled yet.
* Go to **System administration > Setup > Monitoring and telemetry parameters.**
* Under **BeTelemetry** tab define the size of the message content that should be monitored (by default this is set to 0, meaning: no content message is monitored).
