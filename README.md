#include <iostream>
#include <string>
#include <ctime>
#include <time.h>

using namespace std;

struct giocatore
{
    string nome,cognome,ruolo;
    int maglia;
};

struct squadra
{
    string nome_sqdr,allenatore;
    giocatore G[50];
    int giocatori,gol,punti;
};

struct campionato
{
    string nome_cmpnt;
    squadra S[50];
    int num_sqdr;
};

void CaricaSquadre(squadra S[], int n)
{

    for(int i=0;i<n;i++){
        cout<<"Nome squadra: "<<i+1<<" ";
        cin>>S[i].nome_sqdr;
        cout<<"Numero giocatori "<<S[i].nome_sqdr<<": ";
        cin>>S[i].giocatori;
        // cout<<"Cognome allenatore "<<S[i].nome_sqdr<<": ";
        // cin>>S[i].allenatore;
        for(int j=0; j<S[i].giocatori && i<n;j++){
        cout<<"Nome giocatore "<<j+1<<": ";
        cin>>S[i].G[j].nome;
        cout<<"Cognome giocatore "<<j+1<<": ";
        cin>>S[i].G[j].cognome;
        cout<<"Numero maglia giocatore "<<j+1<<": ";
        cin>>S[i].G[j].maglia;
        cout<<"Ruolo giocatore "<<j+1<<": ";
        cin>>S[i].G[j].ruolo;
        }
    }
}

void VisualizzaSquadre(squadra S[], int n)
{

    for(int i=0;i<n;i++){
        cout<<"La Squadra "<<S[i].nome_sqdr;
        cout<<", allenata dal mister "<<S[i].allenatore;
        cout<<", possiede una rosa formata da "<<S[i].giocatori<<" giocatori, "<<endl;
        cout<<"Ecco tutti i giocatori: "<<endl;
        for(int j=0;j<S[i].giocatori && i<n;j++){
            cout<<"Giocatore "<<j+1<<" --> ";
            cout<<"  Nome: "<<S[i].G[j].nome;
            cout<<" Cognome: "<<S[i].G[j].cognome;
            cout<<" Numero Maglia: "<<S[i].G[j].maglia;
            cout<<" Ruolo: "<<S[i].G[j].ruolo<<endl;
        }

    }
}

void VisualizzaClassifica(squadra S[],int n)
{
    for(int i=0;i<n;i++){
        cout<<S[i].nome_sqdr<<" "<<i+1<<" in classifica ";
        cout<<"con "<<S[i].punti<<" punti "<<endl;
}
}


void OrdinamentoClassifica(squadra S[], int n)
{
    bool scambio=true;
    while(n>1 && scambio==true)
    {
        scambio=false;
        int i=0;
        while(i<n-1)
        {
            if(S[i].nome_sqdr>S[i+1].nome_sqdr)
            {
                squadra app=S[i];
                S[i]=S[i+1];
                S[i+1]=app;
                scambio=true;
            }

            i++;
        }
        n--;
    }
}

void OrdinamentoClassificaDpPartita(squadra S[], int n)
{
    bool scambio=true;
    while(n>1 && scambio==true)
    {
        scambio=false;
        int i=0;
        while(i<n-1)
        {
            if(S[i].punti<S[i+1].punti)
            {
                squadra app=S[i];
                S[i]=S[i+1];
                S[i+1]=app;
                scambio=true;
            }

            i++;
        }
        n--;
    }
}

void EliminaString(squadra S[],int &n, string x)
{
    for(int i=0;i<n;i++){
        if(S[i].nome_sqdr==x){
            for(int p=i;p<n-1;p++){
                S[p]=S[p+1];
            }
            n--;
            i--;
        }
    }
}

void EliminaInt(squadra S[],int &n, int x)
{
    for(int i=0;i<n;i++){
        if(S[i].gol==x){
            for(int p=i;p<n-1;p++){
                S[p]=S[p+1];
            }
            n--;
            i--;
        }
    }
}

void ChiHaSegnato(squadra S[], int n, int c)
{
    int i,f,j;
    srand(unsigned(time(NULL)));
    S[i].giocatori=f;
    
    for (int i=0;i<c && j<n;i++){
         int a=rand()%f;
        cout<<"Goal numero "<<i+1<<" segnato da "<<S[a].G[j].nome;   
    }
}


void Partite(squadra S[], int n) //numero squadre
{
    int a,b,c,d;

    srand(unsigned(time(NULL)));
 
    for(int i=0;i<n/2;i++){
   
    c=rand()%(n/2);
	d=rand()%n;

    while(c==d){
        c=rand()%(n/2);
	    d=rand()%n;

    };

    cout<<S[c].nome_sqdr<<" vs "<<S[d].nome_sqdr<<endl;

    a=rand()%10;
    b=rand()%10;

    cout<<"Goal "<<S[c].nome_sqdr<<" "<<a<<endl;
    cout<<"Goal "<<S[d].nome_sqdr<<" "<<b<<endl;
    
  /*  ChiHaSegnato(S,n,a);
    ChiHaSegnato(S,n,b);
   */ 
    

    if (a>b){
        cout<<"Vittoria: "<<S[c].nome_sqdr<<endl;
        S[c].punti=S[c].punti+3;
        S[d].punti=S[d].punti+0;
    }
    else if(a<b){
        cout<<"Vittoria: "<<S[d].nome_sqdr<<endl;
        S[c].punti=S[c].punti+0;
        S[d].punti=S[d].punti+3;
    }
    else{
        cout<<"Pareggio"<<endl;
        S[c].punti=S[c].punti+1;
        S[d].punti=S[d].punti+1;
    }
}
}

int main(){

    squadra S[25];
    campionato C[20];
    int squadre,i,c,d;

    cout<<"Nome campionato: ";
    cin>>C[i].nome_cmpnt;

    cout<<"Inserisci Numero squadre (pari): ";
    cin>>squadre;
    
    while(squadre%2){
        cout<<"Inserisci Numero squadre (pari): ";
        cin>>squadre;
    };

    CaricaSquadre(S,squadre);
    OrdinamentoClassifica(S,squadre);

    Partite(S,squadre);
    OrdinamentoClassificaDpPartita(S,squadre);
    VisualizzaClassifica(S,squadre);



return 0;

}
