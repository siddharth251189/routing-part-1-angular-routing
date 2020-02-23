# Angular Routing

## Router imports

The Angular Router is an optional service that presents a particular component view for a given URL. It is not part of the Angular core. It is in its own library package, @angular/router. Import what you need from it as you would from any other Angular package.
```
import { RouterModule, Routes } from '@angular/router';
```

## Configuration

### app.module.ts
```
import { Routes, RouterModule } from '@angular/router';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';


import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { UsersComponent } from './users/users.component';
import { ServersComponent } from './servers/servers.component';
import { UserComponent } from './users/user/user.component';
import { EditServerComponent } from './servers/edit-server/edit-server.component';
import { ServerComponent } from './servers/server/server.component';
import { ServersService } from './servers/servers.service';

const appRoutes:Routes=[
  {path:'',component:HomeComponent},
  {path:'users',component:UsersComponent},
  {path:'servers',component:ServersComponent}
]

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    UsersComponent,
    ServersComponent,
    UserComponent,
    EditServerComponent,
    ServerComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    RouterModule.forRoot(appRoutes)
  ],
  providers: [ServersService],
  bootstrap: [AppComponent]
})
export class AppModule { }

```
## Router Outlet
After configure the routes in the app.module.ts file we need to add router outlet into our view file as following below:

### app.component.html
```
<div class="container">
<div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>

</div>

```

## Router Link
We use routerLink on place of href into <a> tag for achieving the one page application functionality(change page without the refresh page) 

```
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <ul class="nav nav-tabs">
        <li role="presentation" class="active"><a routerLink="/">Home</a></li>
        <li role="presentation"><a routerLink="servers">Servers</a></li>
        <li role="presentation"><a routerLink="users">Users</a></li>
      </ul>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
  </div>

</div>

```

## Styleing Active Router Link
For styleing active router link we need to add a active class to link and with help of routerLinkActive we can achive this goal but there will be an issue if user will click on another link, default link also will be styled as active link so for solveing the issue we need to add [routerLinkActiveOptions]="{exact:true}" on default router link.

### Important syntax:
#### routerLinkActive="className"
#### [routerLinkActiveOptions]="{exact:true}"

 ```
 <ul class="nav nav-tabs">
        <li
         role="presentation"
          routerLinkActive="active" 
          [routerLinkActiveOptions]="{exact:true}">
          <a routerLink="/">Home</a>
        </li>
        <li 
        role="presentation" 
        routerLinkActive="active">
        <a routerLink="servers">Servers</a>
      </li>
        <li 
        role="presentation" 
        routerLinkActive="active">
        <a routerLink="users">Users</a>
      </li>
      </ul>
```
## Navigating Programmatically
For navigate Programmatically we need to follow steps as given below:

### Steps:

1. Import Router from @angular/router.
2. Call the router in constructor.
3. Use navigate mathod.

### Important syntax:
this.router.navigate(['servers'])

### HTML
```
<button class="btn btn-primary" (click)="onLoadServers()">Load Server</button>
```
### Angular Cord

```javascript
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit {

  constructor(private router:Router) { }

  ngOnInit() {
  }
  onLoadServers(){
    this.router.navigate(['servers'])
  }
}

```
