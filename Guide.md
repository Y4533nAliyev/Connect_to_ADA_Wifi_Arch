# Connect_to_ADA_Wifi_Arch

This is a guide on how to connect to ADA university's Wi-fi on Arch. 

Modern Linux distributions (including Arch and newer Fedoras) use OpenSSL 3, which strictly blocks older TLS versions and legacy renegotiation by default. Many university RADIUS servers are running older software that relies on this legacy tech for PEAP.

# Use Advanced Network Configuration(GUI) and `nmcli`(CLI)

## 1. (I) Advanced Network Configuration

- Open Advanced Network Configuration
- Click the plus icon to set up a connection
- Choose Wi-fi as the connection type
- Give any connection name you want "ADA_Campus" is recommended
- Type "ADA_Campus" on the SSID
- Head to W-ifi-Security and choose `Wpa/Wpa2 Enterprise` in Security
- Choose `PEAP` in Authentication
- **Choose No CA certificate is required**
- Choose `MSCHAPv2` in Inner Authentication
- Type your Username and Password.
- Save and it will try to connect.

If it connects, Congratulation! if not follow the steps below.

## (II) `nmcli`

- Open up a terminal and type `nmcli connection edit ADA_Campus`
- After that you will be taken into `nmcli>`

```
nmcli connection modify "ADA_Campus" wifi-sec.key-mgmt wpa-eap 

nmcli connection modify "ADA_Campus" 802-1x.eap peap 
nmcli connection modify "ADA_Campus" 802-1x.phase2-auth mschapv2

nmcli connection modify "ADA_Campus" 802-1x.identity "YOUR_USERNAME"
nmcli connection modify "ADA_Campus" 802-1x.password "YOUR_PASSWORD" 

nmcli connection modify "ADA_Campus" 802-1x.system-ca-certs no 
nmcli connection modify "ADA_Campus" 802-1x.domain-suffix-match "" 

nmcli connection modify "ADA_Campus" 802-1x.phase1-auth-flags 32 
nmcli connection modify "ADA_Campus" 802-1x.phase1-peapver 0 

nmcli connection up "ADA_Campus"

```

After this you should be able to connect to the Wi-fi. :D

