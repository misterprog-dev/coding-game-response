créer un composant Angular nommé DisplayComponent et
ayant display-component pour sélecteur.

il doit utiliser le composant VoterComponent(sélecteur=voter-component) dont le code est fourni.
DisplayComponent a 3 champs public nommés question,yesAnswer et noAnswer.

ils représentent une question posée à
l'utilisateur et les choix de réponses possibles affichés dans VoterComponent.

DisplayComponent doit utiliser VoterComponent en tant qu'enfant et doit lui passer
question,yesAnswer et noAnswer en entrée.

Quand l'utilisateur vote,VoterComponent créé un événement de type boolean vers un @Output
nommé output.

Je dois afficher le résultat du vote dans DisplayComponent dans un <div> avec id=lastVote:Si output
est vrai,alors on affiche yesAnswer,sinon on affiche noAnswer.

import{Component,Input,NgModule,Output,EventEmitter } from '@angular/core';
 
@component({
       selector:'display-component',
       template:'
 
      '
 
})
 
export class DisplayComponent {
    public question="Too easy?"
    public yesAnswer="Yes";
    public noAnswer="no";
  }
 
// ne pas changer
@component({
    selector:'voter-component',
    template:
    {{question}}
 <button (click)="vote(true)">{{yesAnswer}}</button>
 <button (click)="vote(false)">{{noAnswer}}</button>
 
})
 
export class VoterComponent {
 
 @Input()
  public question:string;
 
 @Input()
  public yesAnswer:string;
 
 @Input()
  public noAnswer:string;
 
@Output()
 public output=new EventEmitter<boolean>();
 
 public vote(vote: boolean):void {
 
    this.output.emit(vote);
    }
 
}