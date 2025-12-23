# 1. Group Information

- **Group Number:** 4
- **Case Study (Project) Title:** Online Food Ordering System
- **Group Members:**
  - _20220719 Sami Khaled Abu Touq_
  - _20220179 Yazan Ahmad Bedair_
  - _20220501 Abdullah Suleiman Jaradat_
  - _20220659 Malek Mahmoud Haj Asad_
- **Course Code, Semester, Instructor:**
  - _13477, first semester, Dr. Samer Elkababji_

# 2. Project Overview

### Purpose and Main Functionalities
**Online Food Ordering System** is a web-based platform connecting customers, restaurants, and delivery agents for seamless food ordering. Customers browse menus and place orders, restaurants manage order confirmations and preparation, and delivery agents track real-time deliveries. The system uses a centralized database with integrated payment gateways and mapping APIs.

### Technologies, Frameworks, and Tools
- _UML and Diagramming:_ PlantUML
- _Development and Documentation:_ VS Code, Pandoc
 
# 3. Diagrams Included

## Use Case Diagrams
- **usecase.puml** - Shows all user interactions including customer, restaurant staff, delivery agent, and admin functionalities.
- **place_order_usecase.puml** - Illustrates the complete order placement workflow from menu browsing to order confirmation.
- **place_order_usecase_tabular_description.md** - Provides detailed tabular documentation for each use case in the order placement process.
- **track_order_and_delivery_usecase.puml** - Demonstrates the order tracking and delivery workflow with real-time GPS tracking.
- **track_order_and_delivery_tabular_description.md** - Contains step-by-step descriptions and scenarios for tracking and delivery use cases.

## Class Diagrams
- **class.puml** - Represents the complete system architecture with all classes including User, Order, MenuItem, Restaurant, and DeliveryAgent.
- **class_user_hierarchy_generalization.puml** - Shows the user hierarchy with generalization from base User class to Customer, RestaurantOwner, DeliveryAgent, and Administrator.
- **class_payment_method_hierarchy.puml** - Models different payment methods using inheritance including CreditCard, DebitCard, DigitalWallet, and CashOnDelivery.
- **class_restaurant_menu_structure.puml** - Represents the restaurant menu organization with categories and menu items.
- **class_order_management_composition.puml** - Demonstrates order structure using composition relationships between Order and its components.

## Sequence Diagrams
- **place_order_sequence_high_level.puml** - Shows the high-level order placement flow between customer, restaurant, and payment service.
- **place_order_sequence_detailed.puml** - Illustrates detailed interactions during order placement including validation, payment processing, and notifications.
- **track_order_&_delivery_sequence_high_level.puml** - Displays the basic tracking workflow for order status and delivery location updates.
- **track_order_&_delivery_sequence_detailed.puml** - Provides comprehensive sequence of tracking interactions including real-time location updates and status notifications.

## Activity Diagram
- **activity_diagram.puml** - Describes the complete workflow for placing and processing an order from browsing to delivery completion.

## State Machine Diagram
- **state_machine_diagram.puml** - Shows order status transitions from Placed → Confirmed → Preparing → Out for Delivery → Delivered.
- **state_stimulus_table.md** - Documents each state and transition with detailed descriptions and business rules.

## Data Flow Diagram
- **DFD.puml** - Demonstrates how data moves between system components including customers, restaurants, payment gateways, and databases.

## Context Diagram
- **context.puml** - Provides a high-level view of the system and its external interactions with customers, restaurants, and third-party services.

# 4. Repository Organization
```
/docs                                             - Project documentation and reports
    se_report_group_04.md                         - Final report
    diagram_explanations.md                       - Markdown documentation for diagrams
    diagram_explanations.pdf                      - PDF version of diagram explanations
    system_description.md                         - System description documentation
    system_description.pdf                        - PDF version of system description

/umls                                             - UML diagrams and models
    /out                                          - Generated output files as svg or HTML
        /activity_diagram                         - Activity diagram outputs
        /class diagrams                           - Class diagram outputs
        /context                                  - Context diagram outputs
        /DFD                                      - Data Flow Diagram outputs
        /place order sequence diagrams            - Place order sequence diagram outputs
        /State Machine Diagram                    - State machine diagram outputs
        /track order & delivery sequence diagrams - Track order & delivery sequence outputs
        /usecase diagrams                         - Use case diagram outputs

    /src                                          - Source UML files
        /class diagrams                           - Class diagram source files
        /place order sequence diagrams            - Place order sequence diagram sources
        /state machine diagram                    - State machine diagram sources
        /track order & delivery sequence diagrams - Track order & delivery sequence sources
        /usecase diagrams                         - Use case diagrams source files
        activity_diagram.puml                     - Activity diagram PlantUML source
        context.puml                              - Context diagram PlantUML source
        DFD.puml                                  - Data Flow Diagram PlantUML source
```

# 5. Team Contributions
The following outlines each team member's responsibilities and contributions to the project:

- **Sami Abu Touq**
  - Designed and implemented UML sequence diagrams:
    - Place Order (High-Level and Detailed)
    - Track Order and Delivery (High-Level and Detailed)
  - Created behavioral modeling diagrams:
    - State Machine Diagram 
    - State Stimulus Table 
    - Activity Diagram 

- **Yazan Bedair**
  - Developed tabular use case descriptions:
    - Place Order
    - Track Order and Delivery
  - Created structural diagrams:
    - User Hierarchy Generalization Class Diagram 
    - Complete Class Diagram 
  - Authored system documentation:
    - System Description

- **Abdullah Jaradat**
  - Created core system diagrams:
    - General Use Case Diagram
    - System Context Diagram
  - Developed specialized class diagrams:
    - Restaurant Menu Structure Class Diagram 
    - Order Management Composition Class Diagram 
  - Authored technical documentation:
    - Diagram Explanations

- **Malek Haj Asad**
  - Defined and documented primary use cases:
    - Place Order Use Case
    - Track Order and Delivery Use Case
  - Created system analysis diagrams:
    - Data Flow Diagram 
    - Payment Method Hierarchy Class Diagram 

## Collaboration Workflow
- Everyone syncs main before starting work
- Each member works on their own branch
- Commit changes with meaningful commits
- Push the branch to GitHub
- Open a Pull Request (PR) from the branch
- At least one teammate reviews before merging
- Merge into main, then delete the branch


