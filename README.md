# Library-Mangement-System
the main objective of this project is provide to search books in a easy manner and for searching , adding , removing books from the Library 
//#include<stdlib.h>
#include<iostream>
#include<string.h>
using namespace std;

#define MAX    100

class bookEntry{
public:
    int copies;
    char name[30];
    char author[30];
};

class library{
public:
    int numBooks;
    bookEntry database[MAX];

    library(){
        numBooks = 0;
    }
    void insertBook( char bookName[], char author[], int c);
    void deleteBook( char bookName[]);
    bookEntry *search( char bookName[]);
};

void library::insertBook( char bookName[], char author[], int c){
    strcpy( database[numBooks].name, bookName);
    strcpy( database[numBooks].author, author);
    database[numBooks].copies = c;
    cout << "Book Inserted Successfully.\n";
    ++numBooks;
}

void library::deleteBook( char bookName[]){
    int i;
    for( i = 0; i < numBooks; i++){
        if( strcmp( bookName, database[i].name) == 0){
            database[i].copies--;
            cout << "Book Deleted Successfully.\n";
            return;
        }
    }
    cout << "Book not found.\n";
}

bookEntry *library::search( char bookName[]){
    int i;
    for( i = 0; i < numBooks; i++){
        if( strcmp( bookName, database[i].name) == 0)
            return &database[i];
    }
    return NULL;
}

int main(){
    library lib;

    char option, name[30], author[30], copies[10];
    while( 1 ){
        cout << "\nEnter your option:\n";
        cout << "I for insert\n";
        cout << "D for delete\n";
        cout << "S for search\n";
        cout << "E for exit\n";

        cin.getline( name, 80);
        option = name[0];

        switch( option){

        case 'i':
            cout << "Enter Name of Book, Author and no of copies per line:\n";
            cin.getline( name, 80);
            cin.getline(author, 80);
            cin.getline(copies, 80);
            lib.insertBook( name, author, atoi(copies));
            break;
        case 'd':
            cout << "Enter Name of Book:\n";
            cin.getline(name, 80);
            lib.deleteBook(name);
            break;
        case 's':
            cout << "Enter Name of Book:\n";
            cin.getline(name, 80);
            bookEntry *item;
            item = lib.search( name );
            if( item != NULL){
                cout << "Book found\n" << item->name << endl << item->author << endl << item->copies << endl;
            }
            else
                cout << "Book not found\n";
            break;
        case 'e':
            exit(0);
            break;
        }
    }
    return 0;
}


