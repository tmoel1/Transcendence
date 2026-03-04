# Transcendence

After two years of low-level C & CPP programming... surprise! Full Stack Web App 🙃

_Co-created with @HaruSnak, @42andy and @Gl1tsh_



**_Below is an abbreviated presentation of the project – for a more complete tour, see: https://github.com/HaruSnak/42-ft_transcendence/_**

---

## So, what is this project about?
The ultimate boss of 42's main cursus, the group project ft_transcendence is somewhat of a deviation from the rest of the cursus, throwing a curveball at students by picking them up and dropping them into an entirly different world of software development: Typescript, Javascript, CSS, HTML, Scripting, all containerised and deplyed via Docker. The base of the project consists of a functional website, with a 1-or-2 player serverside 'Pong' game embedded, and a wide gammut of implementable features such as a inter-user chat/DM and interaction features including multi-user tournements, account creation and modification with strict fencing enforcing best practices, login auth with JWT, persistant game and account statistics, databases, site monitoring/statistics and security features.

## Okay, but what did you actually do?

After having split up the base and optional components between the four of us working on the project, my job was to implement, test and integrate a comprehensive monitoring and analytics suite consisting of a modular ELK stack (ElasticSearch, LogStash & Kibana) and manage the security risks around the website itself, account creation/login, chat feature abuse and database security. 

One goal was to create dashboards consistent across Docker deployments in Kibana, integrating LogStash throughout the codebase wherever relevant to generate and send to ElasticSearch, configured to categorise and stock the information coming in, in a way that Kibana could display and visualise in a more "human-friendly" way. This stack allowed for a system that concurrently permitted extensive analytics data collection AND practically real-time events monitoring, with particular emphasis on those categorised as potential security threats. The dashboarding was integral to filtering and visualisaing the abundence of metrics being collected while the site was active and being used, and an enormeous boon in both testing and presenting the project during the evaluations. Securisation involved manually coded safeties against SQL injection, database protection, ability of users to limit communication with others and more.

The second goal centered on implementing robust security measures throughout the stack to protect against common web vulnerabilities. SQL injection prevention was handled through multi-pattern detection that catches dangerous keywords and syntax, logging every attempt to the ELK stack with full context including IP addresses and attack payloads for forensic analysis. XSS protection strips HTML tags, blocks javascript: protocols, and removes event handlers from all user inputs, while strict regex whitelisting ensures usernames and messages contain only safe characters. Authentication uses JWT tokens with unique identifiers that enable precise revocation tracking, paired with bcrypt password hashing and a rate limiter that caps login attempts at 5 per minute per IP to stop brute-force attacks. The application enforces TLS 1.2/1.3 encryption with strong ciphers and implements CORS to restrict API access to authorized origins only. Network isolation via separate Docker networks (app_network, elk_network, promgraf_network) ensures services can only communicate through defined boundaries. Security events—injection attempts, failed logins, authorization violations—flow through Logstash to Elasticsearch where Prometheus monitors for suspicious patterns and triggers alerts when request rates or resource usage exceed safe thresholds. This created a practical security posture that was both demonstrable during evaluations and effective at stopping real attack vectors, with the added benefit of generating rich audit trails that could be visualized in Grafana alongside the application metrics.

Finally, I collaborated partly on the Prometheus/Grafana stack, which was used to display more real-time information as well as the status of the project and the host machine, to further differentiate it from the ELK stack.

_Feedback welcome_!
