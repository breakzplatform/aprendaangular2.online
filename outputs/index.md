---
layout: default
title: Outputs
edit_link: https://github.com/joselitojunior1/aprenda-angular2/edit/gh-pages/outputs/index.md
tweet: "Utilizando seus próprios eventos loucos usando Outputs no Angular 2"
---

_Atualizado em 16 de Julho de 2016_

Se você deseja vincular um determinado evento, você pode usar o novo [Event sintax]({{ site.baseurl }}/events) no angular 2, mas e se você precisar de um evento personalizado?

Para criar um evento personalizado (custom event), podemos usar o novo decorator `@Output`. Vamos pegar o exemplo do seguinte componente:

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'user-profile',
  template: '<div>Olá, meu nome é {{user.name}}</div>'
})
export class PersonInfo {
  constructor() {}
}
```

Basta importarmos o `Output` e` EventEmitter` do core e criarmos o nosso novo evento

```javascript
import { Component, Output, EventEmitter } from 'angular2/core';

@Component({
  selector: 'user-profile',
  template: '<div>Olá, meu nome é {{user.name}}</div>'
})
export class UserProfile {
  @Output() userUpdated = new EventEmitter();

  constructor() {
    // Atualiza usuário
    // ...
    this.userUpdated.emit(this.user);
  }
}
```

Agora quando utilizamos este componente em outros lugares em nossa aplicação, podemos vincular o evento que emite `person-info`

```html
  <user-profile (userUpdated)="userUpdated($event)"></user-profile>
```

```javascript
export class SettingsPage {
  constructor(){}

  userUpdated(user) {
    // método que manipula o evento
  }
}
```
