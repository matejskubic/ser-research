For on-premises environment all the security prerequisites (firewall, VPNs, …) that are required in order for D365FO and Yokoy solution to be connected should be ensured. This means:
* for API requests from D365FO to Yokoy, a firewall needs to allow HTTPS traffic from D365FO to Yokoy public incoming IP,
* for API requests from Yokoy to FO, a firewall needs to allow HTTPS traffic from public outgoing Yokoy IP to D365FO and ADFS HTTPS endpoints.
