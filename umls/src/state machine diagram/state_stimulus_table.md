# State-Stimulus Table: Online Food Ordering System


## Main State Transitions

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **[Initial]** | Customer adds item to cart | - | Create shopping session | Shopping Cart (ItemsInCart) |

---

## Shopping Cart States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Items In Cart** | updateCartItem() | - | Recalculate total | Cart Modified |
| **Cart Modified** | itemUpdated | - | Update cart display | Items In Cart |
| **Items In Cart** | proceedToCheckout() | - | Initiate checkout process | Cart Reviewed |
| **Cart Reviewed** | continueShoppingSelected | - | Return to shopping mode | Items In Cart |
| **Shopping Cart** | confirmOrder() | - | Generate OrderID | Order Placed (Awaiting Payment) |
| **Shopping Cart** | cartAbandoned | timeout > 30min | Release items | [Terminal] |

---

## Order Placed - Payment States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Awaiting Payment** | initiatePayment() | - | Start payment gateway | Payment Processing |
| **Payment Processing** | paymentSuccess | - | Store transaction details | Payment Verified |
| **Payment Processing** | paymentFailed | - | Log failure details | Awaiting Payment |
| **Order Placed** | paymentCompleted | - | Notify restaurant | Pending Confirmation |
| **Order Placed** | paymentTimeout | time > 15min | Release order resources | Cancelled |
| **Order Placed** | customerCancelRequest | within 2min | Cancel order | Cancelled |

---

## Confirmation States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Pending Confirmation** | restaurantAccepts | - | Update status, notify customer | Confirmed |
| **Pending Confirmation** | restaurantRejects | - | Initiate refund process | Rejected |
| **Pending Confirmation** | confirmationTimeout | time > 10min | Auto-refund | Cancelled |

---

## Confirmed State

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Confirmed** | restaurantStartsPreparation | - | Update ETA | Preparing (In Kitchen) |

---

## Preparing - Kitchen States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **In Kitchen** | cookingComplete | - | Move to inspection | Quality Check |
| **Quality Check** | qualityApproved | - | Begin packaging | Packaging |
| **Quality Check** | qualityFailed | - | Remake item | In Kitchen |
| **Packaging** | packagingComplete | - | Mark ready | [Exit Preparing State] |
| **Preparing** | preparationComplete | - | Assign delivery agent | Ready For Pickup |
| **Preparing** | criticalIssue | - | Full refund | Cancelled |

---

## Ready For Pickup State

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Ready For Pickup** | agentAssigned | - | Notify agent | Out For Delivery (Agent Assigned) |

---

## Out For Delivery - Delivery States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Agent Assigned** | agentAcceptsAssignment | - | Update tracking | Agent En Route to Restaurant |
| **Agent En Route to Restaurant** | agentArrivesAtRestaurant | - | Prepare for handoff | At Restaurant |
| **At Restaurant** | orderCollected | - | Verify items | Order Picked Up |
| **Order Picked Up** | agentDepartsRestaurant | - | Start GPS tracking | En Route to Customer |
| **En Route to Customer** | agentArrivesAtCustomer | - | Prepare for delivery | Arrived at Location |
| **Out For Delivery** | deliveryConfirmed | - | Complete transaction | Delivered |
| **Out For Delivery** | deliveryAttemptFailed | attempts >= 3 | Mark as failed | Delivery Failed |

---

## Terminal States

| Current State | Stimulus/Event | Condition | Action(s) | Next State |
|--------------|----------------|-----------|-----------|------------|
| **Delivered** | customerConfirmsReceipt | - | Request feedback | Completed |
| **Completed** | - | - | Archive order | [Final State] |
| **Cancelled** | - | - | Process refund if needed | [Final State] |
| **Rejected** | - | - | Complete refund | [Final State] |
| **Delivery Failed** | - | - | Handle compensation | [Final State] |

---
