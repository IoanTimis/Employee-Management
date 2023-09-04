#include <iostream>
#include <windows.h>
#include <vector>
#include <fstream>
#include <string>


using namespace std;

class Persoana
{
    protected:

        string nume;
        string prenume;
        int varsta;

    public:

        void setnume(string _nume);
        string getnume();

        void setprenume(string _prenume);
        string getprenume();

        void setvarsta(int _varsta);
        int getvarsta();
};

class Angajat: public Persoana
{
    protected:

        string post;
        int salariu;
        int id;

    public:

        friend istream& operator >> (istream& is, Angajat& var );

        void setpost(string _post)
        {
            post = _post;
        }
        string getpost()
        {
            return post;
        }

        void setsalariu(int _salariu)
        {
            salariu = _salariu;
        }
        int getsalariu()
        {
            return salariu;
        }

        void setid(int _id)
        {
            id = _id;
        }
        int getid()
        {
            return id;
        }

        void afisare();

};

void Angajat::afisare()
    {
        cout << "\033[31mID:" << getid() << ", Numele: " <<  getnume() << ", Prenumele: " << getprenume() << ", Varsta: " << getvarsta() <<
         " de ani, Postul: " << getpost() << ", Salariul: " << getsalariu() <<" de lei";
    }


istream& operator >> (istream& is, Angajat& var )
{
    //is >> var.nume >> var.prenume >> var.post >>var.salariu >> var.varsta >> var.id;
    if(&is == &cin)
    cout << "Nume: \n";
    is >> var.nume;
    if(&is == &cin)
    cout << "Prenume: \n";
    is >> var.prenume;
    if(&is == &cin)
    cout << "Post: \n";
    is >> var.post;
    if(&is == &cin)
    cout << "Salariu: \n";
    is >> var.salariu;
    if(&is == &cin)
    cout << "Varsta: \n";
    is >> var.varsta;
    if(&is == &cin)
    cout << "Id: \n";
    is >> var.id;



    return is;
}


void Persoana::setnume(string _nume)
{
    nume = _nume;
}
string Persoana::getnume()
{
    return nume;
}

void Persoana::setprenume(string _prenume)
{
    prenume = _prenume;
}
string Persoana::getprenume()
{
    return prenume;
}

void Persoana::setvarsta(int _varsta)
{
    varsta = _varsta;
}
int Persoana::getvarsta()
{
    return varsta;
}

vector<Angajat> angajati;

void citireFisier(char* _fisier)
{
    ifstream f(_fisier);
    int n;
    f >> n;
    for(int i = 0; i < n; ++i)
    {
        Angajat citit;
        f >> citit;
        angajati.push_back(citit);
    }

}

void scriereFisier(char* _fisier)
{
    ofstream f(_fisier);
    f << angajati.size() << "\n";
    for(int i = 0; i < angajati.size(); ++i)
    {
        f << angajati[i].getnume() << "\n" << angajati[i].getprenume() << "\n" << angajati[i].getpost() <<
         "\n" << angajati[i].getsalariu() << "\n" << angajati[i].getvarsta() << "\n" << angajati[i].getid() << "\n";
    }
}

void afisareMeniu()
{
    system("cls");
    cout << "\033[36m------------------------------------------------------------------------------------------------------------------------\n";
    cout << "Optiuni:\n"
    "\033[36m1. Adauga Angajat\n"
    "2. Cauta Angajat\n"
    "3. Sterge Angajat\n"
    "4. Afisare Angajati\n"
    "5. Actualizare Angajat\n"
    "6. Afisare Owner\n"
    "7. Exit\n";

    cout << "------------------------------------------------------------------------------------------------------------------------\n";
}

void adauga()
{
    Angajat nou;
    cout << "Adaugare angajat!\n";
    cin >> nou;
    angajati.push_back(nou);
}

void cauta()
{
    Angajat cauta;
    cout << "Cautare angajat!\n";
    cout << "Pentru a trece peste o optiune de cautare,introduceti caracterul \"*\" pentru litere si pentru numere \"0\"\n";
    cin >> cauta;
    int gasit = -1;

    for(int i = 0; i < angajati.size(); ++i)
        {
            if(cauta.getnume()== "*" || cauta.getnume() == angajati[i].getnume())
                {
                    if(cauta.getprenume() == "*" || cauta.getprenume() == angajati[i].getprenume())
                    {
                        if(cauta.getpost() == "*" || cauta.getpost() == angajati[i].getpost())
                        {
                            if(cauta.getsalariu() == 0 || cauta.getsalariu() == angajati[i].getsalariu())
                            {
                                if(cauta.getvarsta() == 0 || cauta.getvarsta() == angajati[i].getvarsta())
                                {
                                    if(cauta.getid() == 0 || cauta.getid() == angajati[i].getid())
                                    {
                                        gasit += 1;
                                        angajati[i].afisare();
                                        cout << '\n';
                                    }
                                }
                            }
                        }
                    }
                }
        }
            if(gasit == -1)
            {
                cout << "Angajatul nu a fost gasit! \n";
            }
            system("pause");
}

void stergere()
{
    cout << "Stergere Angajat!\n";
    cout << "Introduce id-ul angajatului pe care vrei sa-l stergi:\n ";
            int id ,gasit = -1;
            cin >> id;
            for(int i = 0; i < angajati.size(); ++i)
            {
                if(id == angajati[i].getid())
                {
                    gasit += 1;
                    angajati.erase(angajati.begin() + i);
                    cout << "Angajatul a fost sters cu suscces! \n";
                    system("pause");
                    break;
                }
            }

            if(gasit == -1)
                {
                    cout << "Angajatul nu a fost gasit! \n";
                    system("pause");
                }
}

void afisare()
{
    for(int i = 0; i < angajati.size(); ++i)
        {
            angajati[i].afisare();
            cout << "\n";
        }

    system("pause");
}

void afisare(int x)
    {
        x += 1;
        cout <<"Afisare Owner: \n";
        cout <<"Numele: Timis, Prenumele: Ioan, Varsta: 21\n";
        system("pause");
    }

actualizare()
{
    cout << "Actualizare angajat\n";
    cout << "Introduce id-ul angajatului pe care vrei sa-l actualizezi:\n ";
    int id,gasit = -1;
    cin >> id;
    for(int i = 0; i < angajati.size(); ++i)
        {
            if(id == angajati[i].getid())
                {
                    gasit += 1;
                    cout << "Actualizare angajat.\n";
                    cin >> angajati[i];
                    cout << "Angajatul a fost actualizat cu succes\n";
                    system("pause");
                    break;

                }
        }

    if(gasit == -1)
        {
            cout << "Angajatul nu a fost gasit! \n";
            system("pause");
        }
}

int main(int argc , char** argv)
{
    system("");
    citireFisier(argv[1]);

    if(argc > 1)
        {
            if(strcmp(argv[2],"afisare" ) == 0)
            {
                afisare();
                return 0;
            }

            if(strcmp(argv[2],"adauga") == 0)
                {
                    Angajat nou;

                    nou.setnume(argv[3]);
                    nou.setprenume(argv[4]);
                    nou.setpost(argv[5]);
                    nou.setvarsta(stoi(argv[6]));
                    nou.setsalariu(stoi(argv[7]));
                    nou.setid(stoi(argv[8]));

                    angajati.push_back(nou);
                    scriereFisier(argv[1]);
                    return 0;

                }

            if(strcmp(argv[2],"cauta") == 0)
            {



                Angajat cauta;

                cauta.setnume(argv[3]);
                cauta.setprenume(argv[4]);
                cauta.setpost(argv[5]);
                cauta.setvarsta(stoi(argv[6]));
                cauta.setsalariu(stoi(argv[7]));
                cauta.setid(stoi(argv[8]));

                int gasit = -1;



                for(int i = 0; i < angajati.size(); ++i)
                {
                    if(cauta.getnume()== "*" || cauta.getnume() == angajati[i].getnume())
                        {
                            if(cauta.getprenume() == "*" || cauta.getprenume() == angajati[i].getprenume())
                            {
                                if(cauta.getpost() == "*" || cauta.getpost() == angajati[i].getpost())
                                {
                                    if(cauta.getsalariu() == 0 || cauta.getsalariu() == angajati[i].getsalariu())
                                    {
                                        if(cauta.getvarsta() == 0 || cauta.getvarsta() == angajati[i].getvarsta())
                                        {
                                            if(cauta.getid() == 0 || cauta.getid() == angajati[i].getid())
                                            {
                                                gasit += 1;
                                                angajati[i].afisare();
                                                cout << '\n';
                                            }
                                        }
                                    }
                                }
                            }
                        }
                }

                if(gasit == -1)
                    {
                        cout << "Angajatul nu a fost gasit! \n";
                    }
                    system("pause");
                    return 0;


                }

            if(strcmp(argv[2],"sterge") == 0)
                {
                    int id = stoi(argv[3]) ,gasit = -1;

                    for(int i = 0; i < angajati.size(); ++i)
                    {
                        if(id == angajati[i].getid())
                        {
                            gasit += 1;
                            angajati.erase(angajati.begin() + i);
                            cout << "Angajatul a fost sters cu suscces! \n";
                            system("pause");
                            break;
                        }
                    }

                    if(gasit == -1)
                        {
                            cout << "Angajatul nu a fost gasit! \n";
                            system("pause");
                        }
                }

            if(strcmp(argv[2],"actualizare") == 0)
                {
                    int id = stoi(argv[3]),gasit = -1;

                    for(int i = 0; i < angajati.size(); ++i)
                        {
                        if(id == angajati[i].getid())
                            {
                                gasit += 1;
                                cout << "Actualizare angajat.\n";
                                angajati[i].setnume(argv[4]);
                                angajati[i].setprenume(argv[5]);
                                angajati[i].setpost(argv[6]);
                                angajati[i].setvarsta(stoi(argv[7]));
                                angajati[i].setsalariu(stoi(argv[8]));
                                angajati[i].setid(stoi(argv[9]));
                                cout << "Angajatul a fost actualizat cu succes\n";
                                system("pause");
                                break;

                            }
                        }

                if(gasit == -1)
                    {
                        cout << "Angajatul nu a fost gasit! \n";
                        system("pause");
                    }
                }
        }

    while(true)
    {
        afisareMeniu();
        int optiune;
        cin >> optiune;
        system("cls");

        if(optiune == 1)
        {
            adauga();
        }
        else if(optiune == 2)
        {
            cauta();
        }
        else if(optiune == 3)
        {
            stergere();
        }
        else if(optiune == 4)
        {
            afisare();
        }
        else if(optiune == 5)
        {
            actualizare();
        }
        else if(optiune == 6)
            {
                afisare(1);
            }
        else if(optiune == 7)
        {
            break;
        }
        else
        {
            cout << "Optiune invalida! Optiuni valide: [1,2,3,4,5,6,7]\n";
            system("pause");
        }

    }

    scriereFisier(argv[1]);
    return 0;
    }
