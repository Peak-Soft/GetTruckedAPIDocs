# Messaging

Real-time messaging between users (e.g., Shipper and Driver).

## Conversations

### Get / Create Conversation

Start a conversation with another user or retrieve an existing one.

**Endpoint**: `POST /conversations`

**Body**:
```json
{
    "user_id": 45
}
```
*(`user_id` is the ID of the other participant)*

### List Conversations

Get all conversations for the authenticated user.

**Endpoint**: `GET /conversations`

---

## Messages

### Get Messages

Retrieve message history for a specific conversation.

**Endpoint**: `GET /conversations/{conversationId}/messages`

### Send Message

**Endpoint**: `POST /conversations/{conversationId}/messages`

**Body**:
```json
{
    "message": "Hello, is the cargo ready?"
}
```

### Mark as Seen

Mark all messages in a conversation as read.

**Endpoint**: `POST /conversations/{conversationId}/seen`
