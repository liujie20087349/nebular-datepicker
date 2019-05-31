# DatepickerNebular

This project was build to show some unexpected results about nb-datepicker in formcontrol validation

you can clone this repo, then execute:


`npm install `

My node version is `8.15.0`, I suggest that you should use the same node version in order to avoid some unrelated issue.

after installed, execute:

`npm start`

you can see the page on browser with: `localhost:4200`

# Reproduce Issue

***This is not an error, just works not as I expected***

1. open the developer tools on your browser or press F12 to see the console

2. click the nb-datepicker input and select a day

3. after that, you can see the output in the console, which is as follows:
```
FormControl {validator: ƒ, asyncValidator: null, _onCollectionChange: ƒ, pristine: true, touched: false, …}
asyncValidator: null
dirty: (...)
disabled: (...)
enabled: (...)
errors: {nbDatepickerParse: {…}}
invalid: (...)
parent: (...)
pending: (...)
pristine: false
root: (...)
status: "INVALID"
statusChanges: EventEmitter {_isScalar: false, observers: Array(0), closed: false, isStopped: false, hasError: false, …}
touched: false
untouched: (...)
updateOn: (...)
valid: (...)
validator: ƒ (control)
value: Wed May 01 2019 00:00:00 GMT+0800 (中国标准时间) {}
valueChanges: EventEmitter {_isScalar: false, observers: Array(0), closed: false, isStopped: false, hasError: false, …}
_onChange: [ƒ]
_onCollectionChange: ƒ ()
_onDisabledChange: [ƒ]
_parent: FormGroup {validator: null, asyncValidator: null, _onCollectionChange: ƒ, pristine: false, touched: false, …}
_pendingChange: false
_pendingDirty: true
_pendingValue: Wed May 01 2019 00:00:00 GMT+0800 (中国标准时间) {}
__proto__: AbstractControl
```

the part of *errors* is:
```$xslt
errors: {
  nbDatepickerParse: {
    value: "2019年5月1日"
  }
}

```


as you can see, the status of the birthDate formControl is ***INVALID***

but if change the locale from ***zh*** to ***en*** in ***app.module.ts***

```$xslt
registerLocaleData(en);

in NgModule providers:

{
      provide: LOCALE_ID, useValue: 'en'
    }
```

the validation of the same form control works OK, *errors* becomes *null* in the birthDate formControl

and if change locale from ***en*** to ***fr***, *errors* come back again
