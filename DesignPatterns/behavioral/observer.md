## Observer

- A Subject maintains a list of Observers.
- When the subject’s data/state changes, it notifies all observers.
- Observers automatically react to changes — no manual polling.

```
class Subject {
  constructor() {
    this.observers = [];
  }
  subscribe(observer) {
    this.observers.push(observer)
  }
  unsubscribe(observer) {
    this.observers = this.observers.filter((item) => item !== observer)
  }
  setTemperature(temp) {
    this.notify(temp);
  }
  notify(temp) {
    this.observers.forEach((observer) => observer.update(temp))
  }
}



class MobileDisplay {
  update(temp) {
    console.log(`Mobile App: Temperature updated to ${temp}°C`);
  }
}


class WebDashboard {
  update(temp) {
    console.log(`Web Dashboard: Temperature now is ${temp}°C`);
  }
}
const subject = new Subject();
const mobile = new MobileDisplay();
const web = new WebDashboard();

subject.subscribe(mobile);
subject.subscribe(web);

subject.setTemperature(25);
```

- subscribe(observer) – Adds an observer to the list.
- unsubscribe(observer) – Removes the observer from the list.
- notify(data) – Notifies all observers with the updated data.
- Observers must implement an update() method to respond to changes.
