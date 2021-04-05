# Guide of basic components from angular

# Sections

<details open="open">
  <summary>Contents table</summary>
  <ol>
    <li>
      <a href="#Read-form-data-form-a-component">Read form data form a component</a>
    </li>
    <li>
      <a href="#Getting-the-current-date">Getting the current date</a>
    </li>
  </ol>
</details>

# Read form data form a component
On the view
```html
<div class="form-group">
  <label>Selecciona la fecha del reporte: </label>
  <input type="text" #fecha name="fecha" class="form-control datepicker" (blur)="dateChangeEvent($event.target.value)" placeholder="Date Picker Here" />
</div>
```
Then on the component
```typescript
dateChangeEvent(date: string): void {
  this.currentDate = date;
  this.getProjects(this.currentAgency, this.currentDate);
}
```
# Getting the current date
Is needed to import first 
```typescript
import { DatePipe } from '@angular/common';
var datePipe = new DatePipe('en-US');
this.currentDate = String(datePipe.transform(new Date(), 'dd-MM-yyyy'));
```
