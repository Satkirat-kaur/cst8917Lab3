# Teams Chat Content Moderation using Azure Logic Apps

This project is part of **CST8917 Lab 3** and demonstrates a Microsoft Teams chat moderation service using **Azure Logic Apps**. The workflow automatically detects inappropriate content in Teams channel messages and sends an email alert to an admin when a policy violation is found.

## Objective

To build a real-time content moderation system using Azure Logic Apps that:
- Monitors Microsoft Teams channel messages
- Detects flagged words such as "idiot"
- Sends an email alert when violations are detected

## Technologies Used

- **Azure Logic Apps (Consumption)**
- **Microsoft Teams Connector**
- **Outlook 365 – Send Email with Options**
- Logic App Condition expressions with `triggerBody()` and `contains()`

## How It Works

1. **Trigger** – The Logic App is triggered when a new message is added to a Teams channel.
2. **Condition Check** – It evaluates if the message body contains flagged words using:
   ```plaintext
   triggerBody()?['body']?['content']
   ```
   with a `contains` check for inappropriate terms like `"idiot"`.
3. **True Path** – If a violation is detected, it sends a formatted email to the admin using “Send email with options”.
4. **False Path** – If no flagged word is found, no action is taken.

## Example Alert Email

The email contains:
- The original message
- A description of the violation
- Response options (e.g., "Choice1", "Choice2", "Choice3")

![Email Screenshot](https://github.com/Satkirat-kaur/cst8917Lab3/blob/main/email-screenshot.png)

## Testing

The Logic App was tested by posting messages in the selected Teams channel:
- A clean message triggered **no email**
- A message containing `"idiot"` triggered the moderation email instantly

## Challenges Faced

- **Expression errors**: Many initial attempts like `triggerOutputs()?['body']['text']` failed due to missing or incorrect field paths.
- **Solution**: Used `triggerBody()?['body']?['content']` after examining the dynamic content available in Logic App designer.

## Lessons Learned

- How to write and test expressions inside Logic App conditions
- How to debug Logic App runs using Run History
- How to format and send structured alert emails with dynamic message content
- Importance of using correct field references from Teams triggers

## Logic App Workflow Screenshot

![Logic App Designer](https://github.com/Satkirat-kaur/cst8917Lab3/blob/main/logic-app-designer.png)

![Flowchart](https://github.com/Satkirat-kaur/cst8917Lab3/blob/main/Flowchart.png)

## Demo Video

[Watch the demo on YouTube](https://youtu.be/TNtplI2vL6s)


## Future Improvements

- Integrate Azure Cognitive Services for advanced language filtering
- Store flagged messages in a SharePoint list or Azure SQL DB
- Add logic for severity levels based on different types of flagged words
- Send real-time Teams alerts in addition to email notifications
