*[Amina opens the deployment terminal]*

Today we are demonstrating how the payment platform updates itself safely while customers continue using the service.

*[Amina deploys the new release to the standby environment]*

A new version is first prepared separately without affecting live customer traffic. This allows the team to confirm the update is healthy before customers are moved onto it.

*[Amina switches customer traffic to the new environment]*

Traffic is now being moved to the updated version. Customers continue using the service while the system watches for signs of failure.

*[Amina introduces the controlled fault]*

We are now simulating a serious failure in the updated version. The important point is that no engineer is manually repairing the system during this stage.

*[The monitoring system detects the failure and rollback begins]*

The platform detected the issue automatically, removed customers from the failing version, and restored the previous stable version without waiting for human intervention.

*[Amina confirms recovery on screen]*

Normal service has now been restored.

*[Nia concludes the demonstration]*

The full recovery completed automatically in 13 seconds. That response time is faster than a human engineer could realistically detect, diagnose, and repair the issue manually.

