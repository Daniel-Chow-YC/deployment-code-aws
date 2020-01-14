## Security group (stateful)
- Security group is stateful - it remembers which IP is allowed
- So if inbound rule specifies the IP, an IP Outbound rule is not necessary (for this specific inbound) because security group remembers where the request is coming from
- So for an inbound rule, an outbound rule is not needed (it is automatic)
- eg club analogy (If your name on the list you can get in. Once you get in you can leave whenever)

## Network ACL (stateless)
- NACL is stateless - in which there is a need to specify outbound rules.
- Network ACL does not work like Security groups
- eg if your name is on a list (for entry) and you get into a building, once you are in you cannot leave unless your name is also on a list to leave

## TCP-high port range
Port range: 1024 - 65535
- Safe to use
- Port is randomly generated from the range, opens to let request in then closes, lets request out again then closes again.
- (Ephemeral port rules)
- HOWEVER, don't open to 0.0.0.0/0 use specific IP
