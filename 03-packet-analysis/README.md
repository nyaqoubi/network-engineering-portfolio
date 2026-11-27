# DNS and TCP troubleshooting

**Status:** Design and examples documented. Lab verification pending.

## Objective
Use Wireshark to distinguish name-resolution problems from transport-layer connectivity issues.

## Lab scope
Use only a personally controlled network or isolated lab and capture only your own traffic. Publish sanitized screenshots rather than raw captures.

## Implementation checklist
- [ ] Capture a successful DNS lookup and TCP session.
- [ ] Query a nonexistent name under the reserved .invalid domain.
- [ ] Observe an unanswered TCP connection in a controlled lab.
- [ ] Record packet numbers and timing.
- [ ] Write an incident analysis for each outcome.

## Useful display filters
- `dns`
- `dns.flags.rcode != 0`
- `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- `tcp.analysis.retransmission`

| Observation | Interpretation |
|---|---|
| DNS response with address | Name resolution succeeded |
| DNS NXDOMAIN | Name does not exist |
| SYN, SYN-ACK, ACK | TCP connection established |
| Repeated SYN without response | Connection attempt unanswered; cause requires further investigation |
| RST | Connection rejected or reset |

## Incident report template
- Symptom:
- Environment:
- Evidence (packet numbers and screenshot):
- Root cause or confirmed observation:
- Next diagnostic step:
- Resolution and retest:

## Evidence
Pending actual captures and findings.

## Sample troubleshooting workflow

| Scenario | Command or action | Wireshark display filter | Expected evidence |
|---|---|---|---|
| DNS baseline | Run `nslookup example.com` | `dns.qry.name == "example.com"` | Query and response with an address |
| DNS name error | Run `nslookup missing.invalid` | `dns.flags.rcode == 3` | NXDOMAIN if the resolver returns it |
| TCP baseline | Connect to a listening TCP service on your lab server | `tcp.stream == N` (replace N with the stream number) | SYN, SYN-ACK, and ACK |
| TCP timeout | In the same lab, connect to a port configured to silently drop incoming TCP | `tcp.analysis.retransmission` | Repeated SYNs with no reply during the capture window |

Start the capture on the client interface before generating traffic. Use Follow TCP Stream or the stream number to isolate a single connection. Record the frame numbers, observed timing, and which conclusions the packets support. A TCP timeout alone does not identify where a packet was dropped.

**Results:** No packet captures or test outcomes recorded.

