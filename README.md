# Hackerrank Solutions

## Attribute Parser
```
#include <iostream>
#include <map>
using namespace std;

map <string, string> tagMap;

void createMap(int &n, string pretag) {
    if(!n) return;
    
    string line, tag, attr, value;
    getline(cin, line);
    
    int i=1;
    if(line[i]=='/') {           // found closing tag
        while(line[i]!='>') i++;
        if(pretag.size()>(i-2))        // update tag
            tag = pretag.substr(0,pretag.size()-i+1);
        else
            tag = "";
    }
    else {                       // found opening tag
        while(line[i]!=' ' && line[i]!='>') i++;
        tag = line.substr(1,i-1);    // update tag
        if(pretag!="") tag = pretag + "." + tag;
        
        int j;
        while(line[i]!='>') { // go through attributes
            j = ++i;
            while(line[i]!=' ') i++;
            attr = line.substr(j,i-j);    // attribute name
            
            while(line[i]!='\"') i++;
            j = ++i;
            while(line[i]!='\"') i++;
            value = line.substr(j,i-j);    // attribute value
            i+= 1;
            
            tagMap[tag + "~" + attr] = value;
        }
    }
    createMap(--n, tag);
}

int main() {
    int n, q;
    cin >> n >> q;
    cin.ignore();
    createMap(n,"");
    
    string attr, value;
    while(q--) {
        getline(cin,attr);
        value = tagMap[attr];
        if(value=="") value = "Not Found!";
        cout << value << endl;
    }
    return 0;
}
```

## Box It!
```
#include<bits/stdc++.h>

using namespace std;

class Box{
    private:
        int l,b,h;
        
    public:
        Box(){
            this->l=0;
            this->b=0;
            this->h=0;
        }
    
        Box(int length, int breadth, int height){
            this->l=length;
            this->b=breadth;
            this->h=height;
        }
        
        Box(Box &B){
            this->l=B.l;
            this->b=B.b;
            this->h=B.h;
        }
        
        int getLength(){
            return this->l;
        }
        
        int getBreadth(){
            return this->b;
        }
        
        int getHeight(){
            return this->h;
        }
        
        long long CalculateVolume(){
            return (long long)this->l*this->b*this->h;
        }
        
        bool operator <(Box &B){
            return this->l<B.l || (this->b<B.b && this->l==B.l) || (this->h<B.h && this->b==B.b && this->l==B.l); 
        }
        
        friend ostream& operator <<(ostream& out, Box B){
             return out<<B.l<<" "<<B.b<<" "<<B.h;   
        }
};


void check2()
{
	int n;
	cin>>n;
	Box temp;
	for(int i=0;i<n;i++)
	{
		int type;
		cin>>type;
		if(type ==1)
		{
			cout<<temp<<endl;
		}
		if(type == 2)
		{
			int l,b,h;
			cin>>l>>b>>h;
			Box NewBox(l,b,h);
			temp=NewBox;
			cout<<temp<<endl;
		}
		if(type==3)
		{
			int l,b,h;
			cin>>l>>b>>h;
			Box NewBox(l,b,h);
			if(NewBox<temp)
			{
				cout<<"Lesser\n";
			}
			else
			{
				cout<<"Greater\n";
			}
		}
		if(type==4)
		{
			cout<<temp.CalculateVolume()<<endl;
		}
		if(type==5)
		{
			Box NewBox(temp);
			cout<<NewBox<<endl;
		}

	}
}

int main()
{
	check2();
}
```
