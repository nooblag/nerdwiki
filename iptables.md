# iptables

## Rules

### Creating rules

Allow current and established connections -

`iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT`

Allow SSH connections to port 22 -

`iptables -A INPUT -p tcp --dport 22 -j ACCEPT`

Allow HTTP connections to port 80 - 

`iptables -A INPUT -p tcp --dport 80 -j ACCEPT`

Drop any other connections (Important to have as last rule!) -

`iptables -A INPUT -j DROP`

If on VPS, insert this as first rule for the `lo` loopback interface -

`iptables -I INPUT 1 -i lo -j ACCEPT`

### Saving rules

Output to a file -

`iptables-save > rules.fw`

### Restoring rules

Input from a file -

`iptables-restore < rules.fw`
