#include<iostream>
using namespace std;

struct SE9{
int rollno ; 
string name;
float sgpa ;
};
//CLASS STUDENT 
class Student {
struct SE9 Stu[6];
public:
void input();
void display(int n);
void seqsearch();
 void bubblesort();
 void insersort();
 void binsearch();
void quicksort(int , int);
int partition( int low , int high );
};

// TO GET INPUT OF THE STUDENTS
void Student :: input(){
for ( int i = 0; i<6; i++){
cout<<"Enter student "<<i+1<<" roll no, name , sgpa : "<<endl;
cin>>Stu[i].rollno >> Stu[i].name >> Stu[i].sgpa;
}
}
// TO DISPLAY STUDENTS INFORMATION
void Student :: display(int n = 6)
{
    cout<<"\n\n The information about students is : "<< endl;
    cout<<"Sr no. Roll no. SGPA Name " << endl;
        for ( int i = 0 ; i<n ; i++)
        {
        cout<< i+1 <<" "<<Stu[i].rollno <<" "<<Stu[i].sgpa<<  "  "<<Stu[i].name<<endl;
        }
}

//TO  DO SEQUENTIALLY SEARCH FOR A PARTICULAR SGPA
void Student :: seqsearch()
{
float grade;
bool flag = 0;
    cout<<"\n Enter the SGPA to be searched : "<<endl;
    cin>>grade;
    for ( int i = 0 ; i<6 ; i++)
    {
    if ( grade == Stu[i].sgpa )
    {
    cout<<Stu[i].rollno <<" "<<Stu[i].sgpa<<" "<<Stu[i].name<<endl;
    flag = 1; 
    }
    }
    if( flag == 0 ) 
    {
    cout<<" ENTERED DATA IS NOT MATCHED!"<<endl;
    }
 }

 // TO SORT THE ROLL NO USING BUBBLE SORT
void Student :: bubblesort()
{
    for ( int i = 6 ; i>=0; i--)
    {
         for( int j = 0 ; j<i-1; j++)
         {
            if (Stu[j].rollno >= Stu[j+1].rollno)
             {
                SE9 temp = Stu[j];
                Stu[j]= Stu[j+1];
                Stu[j+1] = temp;
              }
         }
    }
 display();
}

// TO SORT NAME OF THE STUDENTS BY INSERTION SORT
void Student :: insersort()
{
    for ( int i = 0 ; i<6; i++)
    {
     SE9 temp = Stu[i];
      int j = i-1;
      while(j>=0 && Stu[j].name > temp.name)
      {
      Stu[j+1] = Stu[j];
      j--;
      }
      Stu[j+1] = temp;
    }
}

// TO PERFORM BINARY SEARCH ON NAME
void Student :: binsearch()
{
    string temp;
    insersort();
    cout<<"\n Enter the name you want to search using binary search : "<<endl;
    cin>>temp;
    int start = 0;
    int end = 5;
    bool flag = 0;
    
    while( start <= end)
    {
    int mid = ( start + end ) / 2;
    if ( Stu[mid].name == temp )
    {
    cout<<Stu[mid].rollno <<" "<<Stu[mid].sgpa<<" "<<Stu[mid].name<<endl;
    flag = 1; 
   break;
    }
    if ( Stu[mid].name < temp ) 
    {start = mid+1;}
    else 
    {end= mid-1;
    }
    }
     if (flag == 0){
       cout<<"Entered name is not Matched with Data "<<endl;
   }
}

//TO DISPLAY THREE TOPPERS FROM CLASS

void Student :: quicksort(int low, int high)
{
if ( low < high )
{
int pivot = partition ( low , high );
quicksort( low , pivot - 1 );
quicksort( pivot + 1 , high );
}
}


int Student :: partition( int low , int high)
{
int pivot = Stu[low].sgpa;
int i = low ;
int j = high ; 
while( i < j )
{
while( Stu[i].sgpa >= pivot && i <= high )
{
i++;
}
while( Stu[j].sgpa < pivot && j >= low )
{
j--;
}
if( i < j )
{
SE9 temp = Stu[i];
Stu[i] = Stu[j];
Stu[j] = temp;
}
}
SE9 temp = Stu[low];
Stu[low] = Stu[j];
Stu[j] = temp;
return j;
}


//MAIN FUNCTION
int main()
{
int op1, op2;
Student obj; 
do
{
cout<<"\n Enter 1 - To take input \n 2 - To display information \n 3 - To search for a sgpa \n 4 - To do bubble sort \n 5 - To do insertion sort \n 6 - To do binary search\n 7 - To do quick sort"<<endl;

cin>>op1;
switch(op1)
{
case 1:
obj.input();
break;

case 2:
obj.display();
break;

case 3:
obj.seqsearch();
break;

 case 4:
 obj.bubblesort();
 break;

 case 5:
 obj.insersort();
obj.display();
 break;

 case 6:
 obj.binsearch();
 break;

case 7:
obj.quicksort(0 , 5);
obj.display(3);
break;

default:
cout<<"Invalid input "<<endl;
}
cout<<"\n PRESS 1  To continue   and 2  To stop \n";
cin>>op2;
}
while(op2==1);
return 0;

}
