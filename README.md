//# DB_Conversion

#include <iostream>
#include <list>
#include <vector>
#include <string>

using namespace std;


void DB1_print(vector<list<list<string>>> &DB1);
void DB1_to_DB2(vector<list<list<string>>> &DB1, list<vector<list<string> * > *> &DB2);
void DB2_print(list<vector<list<string> * > *> &DB2);
void DB2_to_DB3(list<vector<list<string> * > *> &DB2, list < list<list<string *> * > > &DB3);
void DB3_print(list < list<list<string *> * > > &DB3);

int main()
{
	vector<list<list<string>>> DB1 =
	{
		{ { "cat", "dog" },{ "duck", "chicken","pig" } },
		{ { "lion", "tiger", "hyena", "leopard" },{ "Zebra", "elephant" },{ "buffalo" } }
	};
	DB1_print(DB1);
	list<vector<list<string> * > *> DB2;
	DB1_to_DB2(DB1, DB2);
	DB2_print(DB2);
	list < list<list<string *> * > > DB3;
	DB2_to_DB3(DB2, DB3);
	DB3_print(DB3);
	getchar();
	getchar();
	return 0;
}
void DB1_print(vector<list<list<string>>> &DB1)
{
	
	cout << endl;
	for (size_t i = 0; i < DB1.size(); i++){

		for (list<list<string>>::iterator it = DB1[i].begin(); it != DB1[i].end(); it++){
			for (list<string>::iterator it1 = (*it).begin(); it1 != (*it).end(); it1++){
				cout << *it1 << " ";
			}
			cout << endl;
		}
		cout << endl;
	}
}

void DB1_to_DB2(vector<list<list<string>>> &DB1, list<vector<list<string> * > *> &DB2)
{

	for (size_t i = 0; i < DB1.size(); i++){
		vector<list<string> *>*v1 = new vector<list<string> *>;
		for (list<list<string>>::iterator it = DB1[i].begin(); it != DB1[i].end(); it++){
			list<string>*pp = new list<string>;
			for (list<string>::iterator it1 = (*it).begin(); it1 != (*it).end(); it1++){
				pp->push_back(*it1);
				}
			v1->push_back(pp);
		}
		DB2.push_back(v1);
	}

}

void DB2_print(list<vector<list<string> * > *> &DB2){
	
	cout << endl;
	for (list<vector<list<string> * > *>::iterator it = DB2.begin(); it != DB2.end(); it++){
		for (size_t i = 0; i < (*it)->size(); i++){
			for (list<string>::iterator it1 = (*it)->at(i)->begin(); it1 != (*it)->at(i)->end(); it1++)
				cout << *it1 << " ";
			cout << endl;

		}
		cout << endl;
	}
}

void DB2_to_DB3(list<vector<list<string> * > *> &DB2, list < list<list<string *> * > > &DB3)
{


	for (list<vector<list<string> * > *>::iterator it = DB2.begin(); it != DB2.end(); it++){
		list<list<string *> *>qq;
		for (size_t i = 0; i < (*it)->size(); i++){
			list<string *>pp;
			for (list<string>::iterator it1 = (*it)->at(i)->begin(); it1 != (*it)->at(i)->end(); it1++){
				string *y = new string(*it1);
				pp.push_back(y);
			}
			list<string *> *tt = new list<string *>(pp);
			qq.push_back(tt);
		}
		DB3.push_back(qq);
	}
}
void DB3_print(list < list<list<string *> * > > &DB3)
{

	cout << endl;
	for (list < list<list<string *> * > >::iterator it = DB3.begin(); it != DB3.end(); it++){
		for (list<list<string *> * >::iterator it1 = (*it).begin(); it1 != (*it).end(); it1++){
			for (list<string *>::iterator it2 = (*it1)->begin(); it2 != (*it1)->end(); it2++){
				cout << **it2 << " ";
			}
			cout << endl;
		}
		cout << endl;
	}
}

//The following is a sample screenshot
//Your output needs to folloiwng idential format
/*

cat dog
duck chicken pig

lion tiger hyena leopard
Zebra elephant
buffalo


cat dog
duck chicken pig

lion tiger hyena leopard
Zebra elephant
buffalo


cat dog
duck chicken pig

lion tiger hyena leopard
Zebra elephant
buffalo
*/
