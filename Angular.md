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
    <li>
      <a href="#Display-de-date-picker">Display de date picker</a>
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
# Display de date picker
On the view
```html
<div class="form-group">
  <label>Selecciona la fecha del reporte: </label>
  <input type="text" #fecha name="fecha" class="form-control datepicker" (blur)="dateChangeEvent($event.target.value)" placeholder="Date Picker Here" />
</div>
```
Then on the component
```typescript
    ngOnInit(){
        $('.datepicker').datetimepicker({
            format: 'DD-MM-YYYY',    //use this format if you want the 12hours timpiecker with AM/PM toggle
            icons: {
                time: "fa fa-clock-o",
                date: "fa fa-calendar",
                up: "fa fa-chevron-up",
                down: "fa fa-chevron-down",
                previous: 'fa fa-chevron-left',
                next: 'fa fa-chevron-right',
                today: 'fa fa-screenshot',
                clear: 'fa fa-trash',
                close: 'fa fa-remove'
            }
         });
        this.getMcSaldoCapitalCarteras();
    }
```
