# InfernalOps Nights: When My Baby Becomes the Sysadmin of My Nightmares

## 1. Red Alert at 2:43 AM

The incident was declared at 2:43 AM. No siren, no Slack notification, just that piercing cry cutting through the apartment like a critical timeout ping. I sit up in bed, eyes still sticky with sleep—or rather, the 47 minutes I'd managed to scrape together since the last wake-up—and I hear that very recognizable boss music playing in my head.

My first reflex? Check my phone. No PagerDuty alerts from my old projects. Just my little 9-month-old system administrator who just escalated a P0 incident: "Sleep service unavailable, immediate intervention required."

Next to me, my husband continues sleeping. Deeply. Like a Windows server that refuses to restart even when you press the power button. I try to shake him: "Honey... the baby..." He mumbles something vaguely resembling "Mmh okay I'll go" then falls back into his digital coma.

Sigh. *git stash* of my own existence, I get out of bed.

## 2. Initial Diagnosis: Pokémon Week

That night was just the nth iteration of a recurring bug that's been going on for over ten days. The pattern is always the same: wake-up every 2 hours maximum, automatic escalation to me (despite having configured an on-call rotation with my husband), and temporary solutions that never hold.

The previous week, first diagnostic hypothesis: rhinopharyngitis. The pediatrician confirmed Monday: "It's a bad cold, but it only lasts a week maximum." Perfect, we've identified the root cause, the fix will come on its own.

Tuesday, baby returns to daycare. The night is dreadful but hey, it's the cold, "it's almost over." Wednesday, the situation degrades. In addition to constant wake-ups, new alert: fever detected. Thursday, same scenario.

Friday, back to the pediatrician for an emergency post-mortem. Verdict: "At daycare, he caught laryngitis. A new bug, independent of the first one."

I looked at the doctor with that expression all DevOps know well: the one you have when the client tells you "But you said it was fixed!" while a completely new service just went down.

Apparently, daycare is like a poorly isolated staging environment: your code works, but as soon as it comes into contact with other applications, it picks up all their bugs. My son collects viruses like Pokémon. _Gotta Catch 'Em All_. And I pray there are no more pokeballs in circulation.

## 3. My Nocturnal Survival Runbook

After months of production incidents, I've developed my own emergency procedures:

### Standard Procedure (70% of cases)
1. **Detection**: Cry → Automatic 30-second timer (sometimes he falls back asleep alone)
2. **Level 1 Escalation**: Attempt to wake husband (success rate: 20%)
3. **Level 2 Escalation**: Direct intervention from primary admin (me)
4. **Temporary Fix**: Migration to his bed + deployment of "nursing" service

### Degraded Procedure (when papa finally intervenes)
My husband has this fascinating ability: he can drag himself out of our bed, land in the baby's, and already be asleep before his head even touches the pillow. Like a server that goes into hibernation mode instantly.

The problem? My baby clearly sees me as a walking refrigerator. When I intervene, he automatically detects the availability of premium service and categorically refuses workaround solutions. Papa = basic cuddling mode sufficient. Mama = direct access to nutritional resources required. Hard to refuse access when your main user is crying at 3 AM and you are literally his critical infrastructure. But it doesn't really help me implement my weaning project.

### Critical Case: Double Incident
The worst scenario is when both systems fail simultaneously. My older one (27 months) has sleep as fragile as mine—a real legacy system sensitive to interference. When he wakes up too (often because of a diaper "overflow" that contaminated his environment), emergency triage is required.

Priority 1: Prevent incident propagation to the second child  
Priority 2: Restore the "sleep" service of the first  
Result: Minimum one hour of cuddling before system stabilization. And me, impossible to sleep with him—my brain stays in monitoring mode.

## 4. The Real Lessons of Family DevOps

At ManoMano, when I organized GameDays with over 50 participants, I thought I had crisis management mastered. Fatal error. Real production incidents happen at home, at night, when all critical systems decide to crash in cascade.

**Notable differences between tech on-call and parental on-call:**

| Tech On-call | Parental On-call |
|---|---|
| Team rotation | Mama-ops 24/7 |
| Documented runbook | Total improvisation |
| Optional post-mortem | Mandatory existential questioning |
| Coffee available | Cold tea on demand |
| End of incident = back to bed | Next "incident" in 47 minutes |

**What I learned:**

**Patience** is not a soft skill. It's a limited system resource that empties with each intervention and recharges very slowly (ideally during naps, but see terms of use).

Family **load balancing** only works if all team members have the same sensitivity to alerts. Spoiler: this is never the case.

**Recurring incidents** always end up resolving themselves... but usually when you've stopped hoping. And often by themselves, without you understanding why.

## 5. Advanced Monitoring: Metrics That Matter

Forget your Grafana dashboards. My real critical metrics:

- **MTTR** (Mean Time To Recovery): Average time to get a baby back to sleep (objective: <20 min, reality: depends on the moon)
- **Sleep Availability**: Percentage of nights without incident (current SLA: 0%, and that's optimistic)
- **Alert Fatigue**: Number of interventions before mama.exe stops responding
- **Technical Debt**: Accumulation of household tasks postponed due to nocturnal incidents

## 6. Permanent Post-mortem

As I write these lines, the little angels have been sleeping peacefully for a long time... No, I'm kidding. It's 10 PM, my tea is cooling next to my keyboard (as always), and my husband is heroically trying to put both brothers to sleep in the next room. I hear complex negotiations with the big one ("No, we're not going to see the trucks now") and vocal debugging attempts on the little one ("Shh shh shh... come on...").

For the first time today—and probably the only time tonight—I have both free hands AND available mind simultaneously. A system architecture miracle I'm not going to waste. So I wonder: will this ever stabilize?

As an ex-Chaos Engineer, I should appreciate unpredictability. In theory, these nocturnal incidents make my family system more resilient. In practice, they just make me more creative in the art of functioning on 3 hours of cumulative sleep.

Finally, a crying baby is like a frustrated user spamming support without being able to describe their bug. My mission: translate these cries into actionable user stories.

But there's something fascinating about this experience: never in my tech career have I had users so demanding, so unpredictable, and yet so... endearing. When your server crashes, you restart it. When your baby cries at 3 AM, you take them in your arms and realize that's exactly where you want to be.

Even exhausted. Even with cold tea. Even knowing the next alert will arrive in a few hours.

## 7. Next Release

Version 2.0 of my family system is scheduled for... no idea. Children never respect roadmaps, and that's fine. Meanwhile, I continue to iterate, debug on the fly, and learn that the best infrastructure is sometimes just a mom who knows how to give cuddles at 3 AM.

**Coming up in this series:** "Debugging a Stressed Mare: My First Lessons in User Empathy"—because after babies, I'm going to tell you how Vazy taught me to understand unspoken needs.

---

*What about you, what's your worst family production incident? Share your parental survival runbooks in the comments—we're all in the same on-call! 🍵*

---

**About Cecilia**: Ex-Chaos Engineer at ManoMano, ex-Cloud Engineer at Ubisoft, future Product Owner and mom of two boys. Between tech GameDays and sleepless nights, I discovered that the real critical systems wear pajamas. This series explores how my technical skills help me (or not) survive parenthood. 🍵