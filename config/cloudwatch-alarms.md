# Amazon CloudWatch Alarms

## Alarm 1 — High CPU
```
Metric:    CPUUtilization
Threshold: > 70% for 5 minutes
Action:    SNS email notification
Purpose:   Detect DoS, CPU exhaustion, runaway process
```

## Alarm 2 — Low CPU
```
Metric:    CPUUtilization
Threshold: < 5% for 15 minutes
Action:    SNS email notification
Purpose:   Detect app crash, DNS failure, silent outage
```

## Alarm 3 — Status Check
```
Metric:    StatusCheckFailed_Instance
Threshold: >= 1
Action:    SNS email notification
Purpose:   EC2 infrastructure health monitoring
```

## SNS Setup
1. Create SNS topic: EC2-Security-Alerts
2. Add email subscription
3. Confirm via AWS verification email
4. Link topic to all three alarms

## Test the alarm
```bash
sudo dnf install -y stress
stress --cpu 2 --timeout 360
# Email arrives within 5 minutes
```
