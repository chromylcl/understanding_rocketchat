# Flow of sendMessage() function:
User clicks "Edit"
    ↓
setEditMessage(message)
    ↓
React enters edit mode
    ↓
textarea filled with old message
    ↓
User changes text
    ↓
Presses Enter
    ↓
sendMessage()
    ↓
detects edit mode
    ↓
handleEditMessage()
    ↓
RCInstance.updateMessage()
    ↓
fetch("/chat.update")
    ↓
Rocket.Chat backend
