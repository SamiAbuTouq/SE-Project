## Use Case: Track Order & Delivery

| **Field**                    | **Details**                                                                                                                                                                                                                                                                                                |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Use Case Name**            | Track Order & Delivery                                                                                                                                                                                                                                                                                     |
| **Primary Actor**            | Customer                                                                                                                                                                                                                                                                                                   |
| **Secondary Actors**         | Restaurant, Delivery Agent, Mapping / GPS API, Notification Service                                                                                                                                                                                                                                        |
| **Description / Goal**       | Allows a customer to monitor an order’s progress in real time from confirmation to delivery, including order status timeline, ETA, notifications, and live delivery tracking, while operational actors update preparation and delivery status.                                                             |
| **Preconditions**            | • Customer has placed a valid order<br>• Order exists with a unique Order ID<br>• Order is in a trackable state (confirmed or later)<br>• Customer has access to order history or tracking link<br>• Notification Service is operational<br>• _(Optional)_ Delivery agent has GPS/location sharing enabled |
| **Postconditions (Success)** | • Customer views complete delivery progress and final status<br>• Delivery timestamp is recorded<br>• Proof of delivery is available<br>• Customer receives delivery confirmation notification<br>• _(Optional)_ Customer confirms and rates delivery<br>• Order is archived after completion              |
| **Postconditions (Failure)** | • Tracking data cannot be retrieved or updated<br>• Live location is unavailable (GPS/API failure)<br>• Notifications may fail or be delayed<br>• System logs the error and informs the customer                                                                                                           |
| **Triggers**                 | Customer selects **Track Order** from order history or opens a tracking notification/link                                                                                                                                                                                                                  |

---

## Main Success Scenario (Basic Flow)

| **Step** | **Actor**            | **Action**                                                                                    |
| -------: | -------------------- | --------------------------------------------------------------------------------------------- |
|        1 | Customer             | Initiates **Track Order** from order history or notification link.                            |
|        2 | System               | Retrieves and displays order tracking details (Order ID, current status, ETA).                |
|        3 | System               | Displays order status timeline (confirmed, preparing, ready, picked up, en route, delivered). |
|        4 | Notification Service | Sends status update notifications as order progresses through stages.                         |
|        5 | Restaurant           | Updates preparation status (preparing → ready for pickup).                                    |
|        6 | System               | Updates tracking timeline with preparation completion.                                        |
|        7 | Delivery Agent       | Accepts order and updates delivery status to **Picked Up**.                                   |
|        8 | System               | Displays delivery agent details (name, contact, vehicle info).                                |
|        9 | Delivery Agent       | Shares live location through GPS tracking.                                                    |
|       10 | Mapping / GPS API    | Provides real-time location and route information.                                            |
|       11 | System               | Displays live delivery map with driver location and updated ETA.                              |
|       12 | Notification Service | Sends **delivery nearby** notification when driver approaches.                                |
|       13 | Delivery Agent       | Completes delivery and updates status to **Delivered**.                                       |
|       14 | System               | Records delivery timestamp and displays proof of delivery.                                    |
|       15 | Notification Service | Sends delivery confirmation notification to customer.                                         |
|       16 | Customer             | _(Optional)_ Confirms delivery and rates delivery experience.                                 |
|       17 | System               | Completes tracking session and archives order.                                                |

---

## Alternative Flow 1: Live Location Not Available

| **Step** | **Actor** | **Action**                                                             |
| -------: | --------- | ---------------------------------------------------------------------- |
|    AF1.1 | System    | Flow diverges at Step 9 (Share live location).                         |
|    AF1.2 | System    | Detects GPS disabled or location data unavailable.                     |
|    AF1.3 | System    | Displays status timeline and ETA without live map.                     |
|    AF1.4 | System    | Continues sending notifications and updates until delivery completion. |

---

## Alternative Flow 2: Notification Delivery Failure

| **Step** | **Actor**            | **Action**                                                                 |
| -------: | -------------------- | -------------------------------------------------------------------------- |
|    AF2.1 | Notification Service | Fails to send status or proximity notification.                            |
|    AF2.2 | System               | Logs notification failure.                                                 |
|    AF2.3 | System               | Allows customer to manually refresh tracking screen to view latest status. |

---

## Alternative Flow 3: Delivery Agent Delay

| **Step** | **Actor**            | **Action**                                               |
| -------: | -------------------- | -------------------------------------------------------- |
|    AF3.1 | Delivery Agent       | Delivery is delayed due to traffic or operational issue. |
|    AF3.2 | System               | Recalculates ETA based on updated route/location.        |
|    AF3.3 | Notification Service | Sends updated ETA notification to customer.              |
|    AF3.4 | System               | Continues tracking with revised timeline.                |

---

## Exception Flows

| **Step** | **Actor**         | **Action**                                                                              |
| -------: | ----------------- | --------------------------------------------------------------------------------------- |
|    EF1.1 | System            | Cannot retrieve order tracking data (invalid order ID or database error).               |
|    EF1.2 | System            | Displays error message and suggests retry later.                                        |
|    EF2.1 | Mapping / GPS API | GPS service becomes unavailable during active tracking.                                 |
|    EF2.2 | System            | Falls back to status-based tracking (text updates) without live map.                    |
|    EF2.3 | System            | Notifies customer that live tracking is temporarily unavailable.                        |
|    EF2.4 | System            | Continues monitoring for GPS service restoration; resumes live tracking when available. |
