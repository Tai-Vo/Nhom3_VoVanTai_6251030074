#include<iostream>
#include<string>
using namespace std;
class Sv {
public:
	string HoVaTen;
	string Lop;
	string Masv;
	string Khoa;
	string Quequan;
	string Ngaysinh;
	int diem;
	void Input();
};
void Sv::Input() {
	cin.ignore(1);
	cout << "Nhap ho va ten cua sinh vien:"; getline(cin, HoVaTen);
	cout << "Nhap lop cua sinh vien:"; getline(cin, Lop);
	cout << "Nhap Id sinh vien:"; getline(cin, Masv);
	cout << "Sinh vien khoa:"; getline(cin, Khoa);
	cout << "Nhap que quan:"; getline(cin, Quequan);
	cout << "Nhap ngay sinh(dd/mm/yyyy):"; getline(cin, Ngaysinh);
	cout << "Nhap diem ren luyen sinh vien(0->100):"; cin >> diem;
	cout << "============================" << endl;
}
struct Node {
	Sv data;
	Node* next; Node* prev;
};
struct List {
	Node* Head; Node* Tail;
	Node* CreateNode(Sv a);
	List();
	void AddHead(Sv a);
	void Output();
	int length();
	void found();
	void remove();
	void sapxep();
	void suadiem();
	void thongke();
	void suathongtin();
	void timkiemtheo();
};
Node* List::CreateNode(Sv a) {
	a.Input();
	Node* p = new Node;
	p->data = a; p->next = NULL; p->prev = NULL;
	return p;
}
List::List() {
	Head = Tail = NULL;
}
void List::AddHead(Sv a) {
	Node* p = CreateNode(a);
	if (Head == NULL) Head = Tail = p; else {
		p->prev = Tail; Tail->next = p; Tail = p;
	}
}
int List::length() {
	int d = 0;
	for (Node* i = Head; i; i = i->next) {
		d += 1;
	}
	return d;
}
void List::Output() {
	cout << "						-----Ket qua in ra:-----" << endl;
	for (Node* i = Head; i != NULL; i = i->next) {
		cout << "Sinh vien ten la:" << i->data.HoVaTen << "	;	" << "	Id cua sinh vien:" << i->data.Masv << endl;
		cout << "Thuoc lop:" << i->data.Lop << "		;	" << "	Khoa:" << i->data.Khoa << endl;
		cout << "Sinh ngay:" << i->data.Ngaysinh << "		;	" << "	Que quan:" << i->data.Quequan << endl;
		cout << "Diem ren luyen sinh vien:" << i->data.diem << endl;
		if (i->data.diem >= 90) cout << "loai xuat sac!" << endl;
		if (i->data.diem < 90 && i->data.diem >= 80) cout << "Loai gioi!" << endl;
		if (i->data.diem < 80 && i->data.diem >= 70) cout << "Loai kha!" << endl;
		if (i->data.diem < 70 && i->data.diem >= 60) cout << "Loai trung binh!" << endl;
		if (i->data.diem < 60 && i->data.diem >= 50) cout << "Loai yeu!" << endl;
		if (i->data.diem < 50) cout << "Loai kem!" << endl;
		cout << "					#########################" << endl;

	}
}
void List::found() {
	string timkiem; string lop; string khoa;
	int tk;
	cout << "Cu phap tim kiem(1.Tim kiem theo Id;2.Tim kiem theo lop;3.Tim kiem theo khoa:"; cin >> tk;
	if (tk == 1) {
		int t = 0;
		cin.ignore(1);
		cout << "Nhap Id sinh vien can tim kiem:";
		getline(cin, timkiem);
		for (Node* i = Head; i; i = i->next) {
			if (i->data.Masv == timkiem) {
				t++;
				cout << "Thong tin ve sinh vien ban can tim-->" << endl;
				cout << "Ho va Ten:" << i->data.HoVaTen << endl;
				cout << "Lop:" << i->data.Lop << "	;	" << "	Khoa:" << i->data.Khoa << endl;
				cout << "Que quan:" << i->data.Quequan << "	;	" << "	Ngay sinh:" << i->data.Ngaysinh << endl;
			}
		} if (t == 0) cout << "Khong co thong tin ve sinh vien nay!" << endl;
	}
	if (tk == 2) {
		int l = 0;
		cin.ignore(1);
		cout << "Nhap lop sinh vien can tim kiem:";
		getline(cin, lop);
		for (Node* i = Head; i; i = i->next) {
			if (i->data.Lop == lop) {
				l++;
				cout << "Thong tin ve sinh vien ban can tim-->" << endl;
				cout << "ID cua sinh vien la:" << i->data.Masv << endl;
				cout << "Ho va Ten:" << i->data.HoVaTen << endl;
				cout << "Lop:" << i->data.Lop << "	;	" << "	Khoa:" << i->data.Khoa << endl;
				cout << "Que quan:" << i->data.Quequan << "	;	" << "	Ngay sinh:" << i->data.Ngaysinh << endl;
				cout << "###############" << endl;
			}
		} if (l == 0) cout << "Khong co thong tin ve sinh vien nay!" << endl;
	}
	if (tk == 3) {
		int k = 0;
		cin.ignore(1);
		cout << "Nhap khoa sinh vien can tim kiem:";
		getline(cin, khoa);
		for (Node* i = Head; i; i = i->next) {
			if (i->data.Khoa == khoa) {
				k++;
				cout << "Thong tin ve sinh vien ban can tim-->" << endl;
				cout << "ID cua sinh vien la:" << i->data.Masv << endl;
				cout << "Ho va Ten:" << i->data.HoVaTen << endl;
				cout << "Lop:" << i->data.Lop << "	;	" << "	Khoa:" << i->data.Khoa << endl;
				cout << "Que quan:" << i->data.Quequan << "	;	" << "	Ngay sinh:" << i->data.Ngaysinh << endl;
				cout << "###############" << endl;
			}
		} if (k == 0) cout << "khong co thong tin ve sinh vien nay!" << endl;
	}
	if (tk != 3 && tk != 1 && tk != 2) cout << "khong co chuc nang nay!(nhap theo cu phap nha!!!)" << endl;
}
void List::remove() {
	string xoa;
	int k = 0;
	int t, l, lk = 0;
	t = length();
	cin.ignore(1);
	cout << "Id sinh vien ma ban muon xoa:"; getline(cin, xoa);
	if (Head == NULL) cout << "Khong co nguoi nao trong danh sach." << endl;
	else {
		if (t == 1) {
			Head = Tail = NULL;
			cout << "Do chi co 'MOT' sinh vien trong danh sach nen nhap bat ky ID nao thi se tu xoa luon de thanh danh sach rong! " << endl; k++;
		}
		else {
			if (Head->data.Masv == xoa) {
				Head->next->prev = NULL; Head = Head->next; k++;
			}
			if (Tail->data.Masv == xoa) {
				Tail->prev->next = NULL; Tail = Tail->prev; k++;
			}
			for (Node* i = Head; i; i = i->next) {
				if (i->data.Masv == xoa) {
					i->prev->next = i->next;
					i->next->prev = i->prev;
					delete i; k++;
				}
			}
		}
	}
	if (k == 0) cout << "Khong sinh vien nay trong danh sach!" << endl; else cout << "Sinh vien nay da bi xoa!" << endl;
}
void List::sapxep() {
	if (Head == NULL) cout << "Danh sach rong nen ko the sap xep!" << endl; else {
		cout << "Danh sach da duoc xep theo thu tu cua Id!" << endl;
		for (Node* i = Head; i; i = i->next) {
			for (Node* j = i->next; j; j = j->next) {
				if (i->data.Masv > j->data.Masv) swap(i->data, j->data);
			}
		}
	}
}
void List::thongke() {
	int xs, g, k, tb, y, ke;
	xs = g = k = tb = y = ke = 0;
	for (Node* i = Head; i; i = i->next) {
		if (i->data.diem >= 90) xs += 1;
		if (i->data.diem < 90 && i->data.diem >= 80) g += 1;
		if (i->data.diem < 80 && i->data.diem >= 70) k += 1;
		if (i->data.diem < 70 && i->data.diem >= 60) tb += 1;
		if (i->data.diem < 60 && i->data.diem >= 50) y += 1;
		if (i->data.diem < 50) ke += 1;
	}
	cout << "So sinh vien loai xuat sac la:" << xs << endl;
	cout << "So sinh vien loai gioi la:" << g << endl;
	cout << "So sinh vien loai kha la:" << k << endl;
	cout << "So sinh vien loai trung binh la:" << tb << endl;
	cout << "So sinh vien loai yeu la:" << y << endl;
	cout << "So sinh vien loai kem la:" << ke << endl;
}
void List::suadiem() {
	string d;
	int r, dem = 0;
	cin.ignore();
	cout << "Nhap id cua sinh vien ban muon sua lai diem ren luyen:"; getline(cin, d);
	for (Node* i = Head; i; i = i->next) {
		if (i->data.Masv == d) {
			cout << "Nhap lai diem ren luyen sinh vien:"; cin >> r;
			i->data.diem = r;
			cout << "Sinh vien ban vua moi sua la:" << i->data.HoVaTen << endl;
			cout << "Co diem ren luyen la:" << i->data.diem << endl;
			dem += 1;
		}
	}
	if (dem == 0) cout << "Id khong ton tai trong danh sach!" << endl;
}
void List::suathongtin() {
	string d; string t; string l; string k; string q; string n;
	int a, dem = 0;
	cin.ignore();
	cout << "Nhap Id sinh vien ban muon sua thong tin:"; getline(cin, d);
	for (Node* i = Head; i; i = i->next) {
		if (i->data.Masv == d) {
			cout << "Ban muon doi thong tin gi?(go theo cu phap:1.ten;2.lop;3.khoa;4.quequan;5.ngaysinh):"; cin >> a;
			if (a == 1) {
				cin.ignore();
				cout << "Ho va ten moi cua sinh vien:"; getline(cin, t);
				i->data.HoVaTen = t;
			}
			if (a == 2) {
				cin.ignore();
				cout << "Lop moi cua sinh vien la:"; getline(cin, l);
				i->data.Lop = l;
			}

			if (a == 3) {
				cin.ignore();
				cout << "Khoa moi cua sinh vien la:"; getline(cin, k);
				i->data.Khoa = k;
			}

			if (a == 4) {
				cin.ignore();
				cout << "Que quan cua sinh vien la:"; getline(cin, q);
				i->data.Quequan = q;
			}

			if (a == 5) {
				cin.ignore();
				cout << "Ngay sinh cua sinh vien la(dd//mm/yyyy):"; getline(cin, n);
				i->data.Ngaysinh = n;
			}
			if (a > 5 or a <= 0) cout << "Khong co chuc nang!" << endl;

			dem += 1;
		}
	}
	if (dem == 0) cout << "Id nay khong ton tai trong danh sach!" << endl;
}
int main() {
	int n;
	List l; Sv a;
	do {
		cout << "==========MENU==========" << endl;
		cout << "0.Ket thuc chuong trinh" << endl;
		cout << "1.Them vao mot sinh vien." << endl;
		cout << "2.In danh sach sinh vien." << endl;
		cout << "3.Nhap danh sach sinh vien." << endl;
		cout << "4.Tim kiem sinh vien." << endl;
		cout << "5.Xem danh sach co bao nhieu sinh vien." << endl;
		cout << "6.Nhap Id sinh vien ban muon xoa:" << endl;
		cout << "7.Sap xep lai danh sach theo thu tu Id." << endl;
		cout << "8.Thong ke xep loai dua vao diem ren luyen sinh vien." << endl;
		cout << "9.Sua lai diem ren luyen cho sinh vien." << endl;
		cout << "10.Sua thong cua sinh vien." << endl;
		cout << "========================" << endl;
		cout << "Moi ban chon:";
		cin >> n;
		switch (n) {
		case 0:
			cout << "Chuong trinh da duoc ket thuc!!!"; break;
		case 1:
			l.AddHead(a); break;
		case 2:
			l.Output(); break;
		case 3:
			int n;
			cout << "So sinh vien ban muon nhap:"; cin >> n;
			for (int i = 1; i <= n; i++) {
				l.AddHead(a);
			}; break;
		case 4:
			l.found(); break;
		case 5:
			cout << "Sanh sach co:" << l.length() << " sinh vien." << endl; break;
		case 6:
			l.remove(); break;
		case 7:
			l.sapxep(); break;
		case 8:
			l.thongke(); break;
		case 9:
			l.suadiem(); break;
		case 10:
			l.suathongtin(); break;
		default:
			cout << "Khong co chuc nang, moi nhap lai theo menu" << endl; break;
		}
	} while (n);
}
