# lab2-container-security

## Docker image size comparison

| Image             | Image Size | Runtime Size |
| ----------------- | ---------- | ------------ |
| my-app:hardened   | 206MB      | 50.4MB       |
| my-app:vulnerable | 1.46GB     | 378MB        |

Det syns ganska tydligt att den härdade imagen är **mycket mindre**, vilket minskar attackytan och gör den snabbare att deploya.

## Test av pods

### Vulnerable pod

<img width="808" height="360" alt="image" src="https://github.com/user-attachments/assets/97273d83-d8ab-4035-b886-ed404116187a" />


### Hardened pod

<img width="432" height="79" alt="image" src="https://github.com/user-attachments/assets/0bfd3040-63e1-4d12-a90d-3f04a111f369" />


## trivy scan results:

### Before:
<img width="800" height="454" alt="image" src="https://github.com/user-attachments/assets/2960b9bd-fccc-4220-9153-c26a9a298d75" />

### After:
<img width="805" height="459" alt="image" src="https://github.com/user-attachments/assets/fd96be95-4726-430f-b1b2-367cc3e99dc2" />


## Reflektion

Jag lärde mig att container-säkerhet inte bara handlar om runtime utan börjar redan vid hur imagen byggs. Mindre images innebär färre beroenden, vilket direkt minskar risken för sårbarheter. Jag såg också hur enkelt det är att råka inkludera onödiga paket som ökar attackytan utan att man tänker på det.

SBOM är viktigt eftersom det ger full insyn i exakt vilka komponenter som finns i en container. Det gör det möjligt att snabbt identifiera sårbarheter och förstå vad som faktiskt körs i produktion. Utan SBOM blir det i princip gissningar när något går fel eller när en CVE dyker upp.

Policy enforcement med Gatekeeper förändrar arbetssättet ganska mycket. Istället för att manuellt granska konfigurationer så tvingas säkerhetsregler igenom automatiskt. Det gör att fel stoppas direkt vid deploy istället för i efterhand. Samtidigt kräver det att man tänker mer på policies från början, annars blir det bara frustration när saker blockeras.
