## Factory 
- The Factory Pattern is a creational design pattern that provides a separate factory class or method to create objects.
- It hides the object creation logic from the client and delegates it to a factory, which can decide which subclass to instantiate based on input or logic.

```
class Notification {
  constructor(message) {
    this.message = message;
  }
  show() {
    console.log("Showing notification: " + this.message);
  }
}



class SuccessNotification extends Notification {
  show() {
    console.log("SUCCESS: " + this.message);
  }
}

class ErrorNotification extends Notification {
  show() {
    console.log("ERROR: " + this.message);
  }
}

class WarningNotification extends Notification {
  show() {
    console.log("WARNING: " + this.message);
  }
}
class NotificationFactory {
  static createNotification(type, message) {
    switch (type) {
      case "success":
        return new SuccessNotification(message);
      case "error":
        return new ErrorNotification(message);
      case "warning":
        return new WarningNotification(message);
      default:
        throw new Error("Invalid notification type");
    }
  }
}

const notif1 = NotificationFactory.createNotification("success", "Data saved!");
const notif2 = NotificationFactory.createNotification("error", "Something went wrong!");
const notif3 = NotificationFactory.createNotification("warning", "Low battery!");

notif1.show(); 
notif2.show(); 
notif3.show();

```

- NotificationFactory handles object creation logic.
- Adding new types (like "info") only requires editing the factory, not the calling code.
- Promotes loose coupling, maintainability, and extensibility.
