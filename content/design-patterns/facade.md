---
title: "Facade with examples in Python"
date: 2024-02-06T23:03:34+05:30
draft: false
showToc: false
TocOpen: false
cover:
    image: img/facade.png
    alt: "facade"
tags: ["design-patterns"]
---

The Facade Design Pattern is like having a remote control for various devices in our home. Imagine we have a TV, a sound system, and lights in our living room. Instead of turning on each one separately, we use a remote control (the "facade") that has a single "movie mode" button. When we press it, the remote turns on the TV, sets the sound system to the right volume, and dims the lights all at once. The remote simplifies the process by providing one button to control everything, instead of us manually managing each device.

In the context of code, a facade is an object that provides a simplified interface to a larger body of code, like a library or a complex system of classes.

Let's understand this with an example:
```python
# Complex parts
class Engine:
    def start(self):
        return "Engine is starting"

class AirConditioner:
    def turn_on(self):
        return "Air conditioner is on"

class Radio:
    def play_music(self):
        return "Playing music"

# Facade
class CarFacade:
    def __init__(self):
        self.engine = Engine()
        self.air_conditioner = AirConditioner()
        self.radio = Radio()

    def turn_on_car(self):
        start_engine = self.engine.start()
        ac_on = self.air_conditioner.turn_on()
        music = self.radio.play_music()
        return f"{start_engine}, {ac_on}, and {music}"

def main():
    car = CarFacade()
    print(car.turn_on_car())

if __name__ == "__main__":
    main()
```

In this example, `CarFacade` acts as the remote control. The `turn_on_car` method is like the "movie mode" button; it starts the engine, turns on the air conditioner, and starts playing music with one command, hiding the complexity of the individual systems behind a simple interface.

The Facade Design Pattern is commonly used in situations where a system is very complex or difficult to understand because it involves a lot of interdependent classes or because its source code is hard to read. In such cases, a facade can provide a simple, easy-to-understand interface over the complex system. Here's a real-world coding scenario where a facade might be used:

**Scenario: Email System Integration**

Imagine we are developing an application that needs to send out emails. The email sending process involves several complex steps:

1. **Preparing the email content**: This may involve using a template system to insert data into predefined templates and formatting the content for plain text and HTML versions.
2. **Attachment handling**: If our email has attachments, they need to be encoded and added to the email.
3. **SMTP configuration**: We need to configure the Simple Mail Transfer Protocol (SMTP) settings, which might include setting up the host, port, user credentials, and encryption methods.
4. **Sending the email**: This involves establishing a connection to the SMTP server, authenticating, sending the email data, and then handling the response.
5. **Error handling**: Proper error handling and logging are necessary to understand if the email was sent successfully or if it failed.

In a large application, each of these steps might be handled by a different class or library, and interacting with them directly can be quite complicated.

**Facade Implementation:**

To simplify this for the rest of our application, we could create a `EmailFacade` class. This facade would provide a simple method such as `send_email`, which would internally handle all of the steps described above. The rest of our application code only needs to know about this facade and can send emails without worrying about the underlying complexities.

Here is an abstract representation of what that might look like in code:

```python
class EmailFacade:
    def __init__(self):
        self.content_creator = EmailContentCreator()
        self.attachment_handler = AttachmentHandler()
        self.smtp_configurator = SMTPConfigurator()
        self.email_sender = EmailSender()
        self.error_handler = EmailErrorHandler()

    def send_email(self, to_address, subject, template, data, attachments=None):
        content = self.content_creator.create_content(template, data)
        email = self.attachment_handler.add_attachments(content, attachments)
        smtp_details = self.smtp_configurator.configure_smtp()
        try:
            self.email_sender.send(smtp_details, to_address, subject, email)
            print("Email sent successfully!")
        except Exception as e:
            self.error_handler.log_error(e)
```

By using the facade, any developer working on the application can send emails easily without having to understand the inner workings of the email system. They just need to know the parameters for the `send_email` method of the `EmailFacade`. This not only makes the developer's life easier but also makes the application more maintainable and less prone to errors.