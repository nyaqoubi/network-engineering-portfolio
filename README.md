# DNS and TCP troubleshooting

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
