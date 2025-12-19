## Use Case: Place Order

| **Field**                    | **Details**                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Use Case Name**            | Place Order                                                                                                                                                                                                                                                                                                                                                                              |
| **Primary Actor**            | Customer                                                                                                                                                                                                                                                                                                                                                                                 |
| **Secondary Actors**         | Restaurant, Payment Gateway, Notification Service                                                                                                                                                                                                                                                                                                                                        |
| **Description / Goal**       | Allows a customer to place a food order by selecting items, configuring delivery details, validating the order, completing payment successfully, and receiving confirmation while notifying the restaurant.                                                                                                                                                                              |
| **Preconditions**            | • Customer is logged in (authenticated session)<br>• Customer account is active and in good standing<br>• Cart contains at least one item<br>• Customer has at least one delivery address or can add a new one<br>• At least one restaurant is available and accepting orders<br>• Payment Gateway is operational                                                                        |
| **Postconditions (Success)** | • Order is created with a unique Order ID<br>• Payment is processed successfully and Transaction ID is recorded<br>• Customer receives order confirmation with ETA<br>• Restaurant receives new order notification<br>• Order status set to **Pending Restaurant Confirmation**<br>• Cart is cleared<br>• Inventory/menu availability updated (if applicable)<br>• Order history updated |
| **Postconditions (Failure)** | • No order is created; payment is refunded if captured<br>• Customer is notified with a clear failure reason<br>• Cart contents are preserved for retry<br>• Restaurant is not notified<br>• Error is logged by the system                                                                                                                                                               |
| **Triggers**                 | Customer clicks **Place Order** from checkout/order summary screen                                                                                                                                                                                                                                                                                                                       |

---

## Main Success Scenario (Basic Flow)

| **Step** | **Actor**            | **Action**                                                                                  |
| -------- | -------------------- | ------------------------------------------------------------------------------------------- |
| 1        | Customer             | Initiates **Place Order**.                                                                  |
| 2        | Customer             | Selects food items from menu and adds them to cart.                                         |
| 3        | Customer             | _(Optional)_ Customizes items (special instructions, add-ons).                              |
| 4        | Customer             | Manages cart (add/remove/update item quantities).                                           |
| 5        | Customer             | Selects or adds delivery address.                                                           |
| 6        | Customer             | _(Optional)_ Schedules order for later delivery.                                            |
| 7        | System               | Displays order summary (items, address, timing, costs).                                     |
| 8        | Customer             | _(Optional)_ Applies coupon or discount.                                                    |
| 9        | Customer             | _(Optional)_ Adds tip.                                                                      |
| 10       | System               | Calculates final order total (prices, tax, delivery fee, discounts, tip).                   |
| 11       | System               | Validates order (restaurant availability, delivery area, minimum order, item availability). |
| 12       | Customer             | Proceeds to make payment.                                                                   |
| 13       | Payment Gateway      | Processes payment and returns success response.                                             |
| 14       | System               | Creates order record and stores payment transaction ID.                                     |
| 15       | Notification Service | Sends order confirmation to customer and order alert to restaurant.                         |
| 16       | Customer             | _(Optional)_ Saves order as favorite.                                                       |
| 17       | System               | Completes order placement successfully.                                                     |

---

## Alternative Flow 1: Payment Failure

| **Step** | **Actor**       | **Action**                                                                                        |
| -------- | --------------- | ------------------------------------------------------------------------------------------------- |
| AF1.1    | System          | Flow diverges at Step 13 of Main Success Scenario (Make Payment).                                 |
| AF1.2    | Payment Gateway | Returns payment failure response (e.g., insufficient funds, invalid card, expired card, timeout). |
| AF1.3    | System          | Displays specific payment error message to customer.                                              |
| AF1.4    | Customer        | Chooses to retry payment, change payment method, or cancel order.                                 |
| AF1.5    | System          | If retry succeeds, resumes Main Success Scenario at Step 14.                                      |
| AF1.6    | System          | If customer cancels, preserves cart and terminates use case with no order created.                |

---

## Alternative Flow 2: Order Validation Failure

| **Step** | **Actor** | **Action**                                                                                               |
| -------- | --------- | -------------------------------------------------------------------------------------------------------- |
| AF2.1    | System    | Flow diverges at Step 11 of Main Success Scenario (Validate Order).                                      |
| AF2.2    | System    | Detects validation failure (restaurant closed, address out of range, minimum not met, item unavailable). |
| AF2.3    | System    | Displays specific validation error message.                                                              |
| AF2.4    | Customer  | Modifies cart, selects different address, or chooses another restaurant.                                 |
| AF2.5    | System    | Returns customer to order summary and resumes flow from Step 7.                                          |

---

## Alternative Flow 3: Cancel Order Before Payment

| **Step** | **Actor** | **Action**                                                        |
| -------- | --------- | ----------------------------------------------------------------- |
| AF3.1    | Customer  | Cancels order at any point before payment confirmation.           |
| AF3.2    | System    | Preserves cart contents for future session.                       |
| AF3.3    | System    | Terminates use case with no order created and no charges applied. |

---

## Exception Flows

| **Step** | **Actor** | **Action**                                                                              |
| -------- | --------- | --------------------------------------------------------------------------------------- |
| EF1.1    | System    | Encounters system or database error while creating the order after successful payment.  |
| EF1.2    | System    | Initiates payment refund and informs customer that the order could not be completed.    |
| EF2.1    | System    | Detects session timeout due to customer inactivity before payment confirmation.         |
| EF2.2    | System    | Saves cart contents and ends session; customer may resume order after logging in again. |
