
Socket System Frontend Integration Guide
========================================

* * *

Overview
--------

This document provides the guidelines and structure for integrating the socket system with the frontend application. It outlines the event structure, types, and actions that frontend developers need to handle to ensure seamless communication between the backend and the frontend.

* * *

Event Structure
---------------

Each event sent or received through the socket system follows a standardized structure:

```javascript
{
"uid": "11", // User ID 
"type": "payment", // Event category
"action": "withdraw", // Specific action within the type
"description": "Withdraw 2000Y from Alipay: channelCode - 101" // Description of the event
}
```

### Field Descriptions

*   **uid** (string): The unique identifier of the user performing the action.
*   **type** (string): The category of the event. Acceptable values are listed below.
*   **action** (string): The specific action related to the event type.
*   **description** (string): A detailed explanation of the event.

* * *

Event Types and Actions
-----------------------

Below is the list of supported event types and their associated actions:

### 1\. Payment

*   **Actions:**
    *   withdraw
    *   recharge
    *   exchange
    *   contact
    *   check\_bill

### 2\. Game

*   **Actions:**
    *   withdraw
    *   deposit
    *   exchange
    *   play
    *   check_balance
    *   check_record

### 3\. Live

*   **Actions:**
    *   watch
    *   tip
    *   comment
    *   search
    *   check\_ranking

### 4\. Video

*   **Actions:**
    *   watch
    *   search

### 5\. VIP

*   **Actions:**
    *   upgrade
    *   read\_book

### 6\. Setting

*   **Actions:**
    *   change_password
    *   edit_info
    *   check_balance
    *   change_language
    *   security
    *   switch_account

### 7\. Promotion

*   **Actions:**
    *   check
    *   use

### 8\. General

*   **Actions:**
    *   login
    *   search
    *   contact_service
    *   contribution

* * *

Integration Instruction Example with JavaScript
------------------------

### 1\. Listening to Events:

Frontend applications should establish a socket connection and listen for incoming events from the backend. The event data will conform to the structure provided above.

**Example:** ```javascript socket.on('event', (data) => { console.log('Received event:', data); handleEvent(data); });```

### 2\. Handling Events:

Create a handler function to process incoming events based on the type and action.

**Example:** 
```javascript 
function handleEvent(event) {
   switch (event.type)
      {
         case 'payment': handlePaymentEvent(event);
         break;
         case 'game': handleGameEvent(event);
         break;
         // Add other cases as needed
         default: console.warn('Unknown event type:', event.type);
       }
 }

function handlePaymentEvent(event) {
   if (event.action === 'withdraw') {
      console.log('Processing withdrawal:', event.description); // Perform frontend logic for withdrawal
       }
};
```

### 3\. Sending Events:

To initiate events from the frontend, follow the same structure and send them through the socket connection.

**Example:** 
```javascript
const event = { uid: '11', type: 'payment', action: 'recharge', description: 'Recharge 5000Y to account via channelCode - 102' };


socket.emit('event', event);
 ```

### 4\. Error Handling:

Ensure to handle any errors or unexpected data gracefully.

**Example:** 
```javascript
socket.on('error', (error) => { console.error('Socket error:', error); });
```

* * *


Conclusion
----------

By following this guide, frontend developers can effectively integrate the socket system into their applications, ensuring efficient and reliable communication with the backend. For any questions or additional support, please contact the backend team.
