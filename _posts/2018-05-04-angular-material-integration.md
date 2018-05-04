---
layout: post
title: Angular પ્રોજેક્ટમાં Material Design કઈ રીતે integrate કરવી?
date: 2018-05-04 16:45:00
author: sanket
---

## Angular Material library
Material Design એક design language છે, જે Google દ્વારા ૨૦૧૪ માં બનાવવામાં આવી. આ design ને developers સરળતા થી Angular project માં ઉપયોગમાં લઇ શકે એ માટે Angular ના જ મૂળ developers દ્વારા Angular Material library બનાવવામાં આવી.

આ library માં ઘણા બધા components બનાવવા માં આવ્યા છે જેને આપને આપણી application માં સરળતાથી ઉપયોગમાં લઇ શકીએ છીએ. આ library અન્ય material layout standards અને best practices નું ધ્યાન રાખી ને બનાવામાં આવી છે જેથી developers ને material specification ની ઉંડાણથી ખબર હોવી જરૂરી રહેતી નથી.

ચાલો તો આપણે Angular Project માં આ mterial design કઈ રીતે add કરવી એ જોઈએ.

## Angular Project બનાવવો

> નીચેના command run થવા માટે આપના machine માં [Angular-Cli](https://cli.angular.io/) અને [Node.Js](https://nodejs.org/en/) install હોવા જરૂરી છે. જો એ ના હોય તો, પહેલા એ install કરી દો.

`ng new <app_name>` command નો ઉપયોગ કરી ને આપણે સરળતાથી angular project બનાવી શકીએ છીએ. ત્યાર બાદ `npm install` commnad દ્વારા બધા packages install કરો (આ command run થતા થોડી મીનીટો લાગશે).

`ng serve` command run કરી એક વખત verify કરી લ્યો કે application બરાબર ચાલે છે ને?

## Angular material અને Angular CDK install કરવું

installation માટે તમે npm અથવા [yarn](https://yarnpkg.com/en/) કોઈ પણ package manager નો ઉપયોગ કરી શકો છો. બંને package manager માટે ના command નીચે મુજબ છે.

NPM :

` npm install --save @angular/material @angular/cdk `

Yarn : 

` yarn add @angular/material @angular/cdk `

## Animation library install કરવી

Material design ના ઘણા components એ Angular Animations module ઉપર આધારિત છે, કે જેના દ્વારા components નું UX સુધારવા માટે જે animation effects વપરાયા હોય એ enable થાય છે. નીચેના command દ્વારા આ library install કરી સકાય છે.

NPM :

` npm install --save @angular/animations `

Yarn : 

` yarn add @angular/animations `

આ Angular animation module ને નીચે મુજબ આપણી application ના root (મુખ્ય) module માં import કરો.

```typescript
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';

@NgModule({
  ...
  imports: [BrowserAnimationsModule],
  ...
})
export class MyAppModule { }
```

## Theme import કરવી
Angular Material library અમુક તૈયાર themes આપે છે, જે આપણી application અમુક મૂળભૂત styles માટે જરૂરી છે. આવી તૈયાર themes ની files `\node_modules\@angular\material\prebuilt-themes` folder માં હોય છે. જેને આપણી application માં ઉપયોગ કરવા માટે `style.css` માં પ્રથમ line માં એને નીચે મુજબ import કરવામાં આવે છે.

` @import "~@angular/material/prebuilt-themes/indigo-pink.css";`

## Angular Material ના તૈયાર components ne આપણી application માં import કરવા
Angular માં દરેક components એને અનુરૂપ કોઈક NgModule માં હોય છે. એજ પ્રમાણે Angular material ના components જેમકે  MatButton એ MatButtonModule માં અને MatCheckbox એ MatCheckboxModule માં આવેલ છે. એમને આપણી application માં ઉપયોગ માં લેવા માટે નીચે મુજબ આ અનુરૂપ modules ને આપણી application ના modules માં import કરવામાં આવે છે.


```typescript
import {MatButtonModule, MatCheckboxModule} from '@angular/material';

@NgModule({
  ...
  imports: [MatButtonModule, MatCheckboxModule],
  ...
})
export class MyAppModule { }
```

સામાન્ય રીતે જયારે application માં ઘણા બધા modules હોય ત્યારે દરેક modules માં આ પ્રમાણે એક એક component મુજબ એને અનુરૂપ modules import કરવું ઘણું વધુ કામ થઇ જાય છે. એના માટે આપણે એક અલગ જ CustomMaterialModule નામનું module બનાવી ને એમાં બધા જ component ને અનુરુપ modules import કરી, પછી આપણી appliation માત્ર આ CustomMaterialModule જ import કરવાનું વધુ સરળતા ભર્યું રહે છે.

> નવું module `ng generate module <module_name>` command દ્વારા બનાવી શકાય.

### જરૂરી એવા બધાજ Angular Material components ને import કરતુ અલગ module
```typescript
import {MatButtonModule, MatCheckboxModule} from '@angular/material';

@NgModule({
  imports: [MatButtonModule, MatCheckboxModule],
  exports: [MatButtonModule, MatCheckboxModule],
})
export class CustomMaterialModule { }
```

### આપણા application module માં તેનો ઉપયોગ નીચે મુજબ કરી શકાય
```typescript
import {CustomMaterialModule} from './custom-material/custom-material.module';

@NgModule({
  imports: [CustomMaterialModule],
})
export class MyAppModule { }
```

## Angular application ના template માં Angular material component નો ઉપયોગ
હવે અંતે આ angular material components આપણી application view પર જોવાનો સમય આવી ગયો છે. જેના માટે component ના template એટલે કે .html file (અથવા તો .ts file ના inline template માં), angular material ને અનુરૂપ html tag લખવાથી એ render થાય છે.

જેમકે MatButton display કરવા માટે,
```html
<mat-button> Click Me! </mat-button>
```

તો આ પ્રમાણે આપણે Angular project માં ખુબ સરળતા થી material theme અને તેના components નો ઉપયોગ કરી ખુબ જ સારી દેખાતી અને standard web application ઝડપથી બનાવી શકીએ છીએ.

આશા રાખું છું કે આપને આ post દ્વારા જરૂરી guidance મળ્યું હશે. તમને Angular, Angular Material અથવાતો programming વિષે કઈ પણ જાણવાની ઈચ્છા કે પ્રશ્નો હોય તો નીચે comments દ્વારા જરૂર થી મને જણાવો. હું video કે blog post દ્વારા બને એટલા જલ્દી આપને એ પ્રશ્નોના જવાબ પહોચાડવાનો પ્રયત્ન કરીશ.

આભાર!
