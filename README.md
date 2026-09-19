#include <iostream>
#include <string>
#include <iomanip>

using namespace std;

struct Date {
    int ngay;
    int thang;
    int nam;
};

struct HangHoa {
    string maHang;
    string tenHang;
    Date ngayXuat;
    double giaXuat;
};

void nhap1HangHoa(HangHoa &h) {
    cout << "Nhap ma hang: ";
    cin.ignore();
    getline(cin, h.maHang);
    cout << "Nhap ten hang: ";
    getline(cin, h.tenHang);
    cout << "Nhap ngay xuat (ngay thang nam): ";
    cin >> h.ngayXuat.ngay >> h.ngayXuat.thang >> h.ngayXuat.nam;
    cout << "Nhap gia xuat (trieu dong): ";
    cin >> h.giaXuat;
}

void nhapDanhSach(HangHoa a[], int n) {
    for (int i = 0; i < n; i++) {
        cout << "\nNhap thong tin hang hoa thu " << i + 1 << ":\n";
        nhap1HangHoa(a[i]);
    }
}

void xuatDanhSach(HangHoa a[], int n) {
    cout << left << setw(15) << "Ma Hang" 
         << setw(25) << "Ten Hang" 
         << setw(15) << "Ngay Xuat" 
         << setw(20) << "Gia Xuat (Trieu)" << endl;
    cout << string(75, '-') << endl;
    for (int i = 0; i < n; i++) {
        string strNgay = to_string(a[i].ngayXuat.ngay) + "/" + 
                         to_string(a[i].ngayXuat.thang) + "/" + 
                         to_string(a[i].ngayXuat.nam);
        cout << left << setw(15) << a[i].maHang 
             << setw(25) << a[i].tenHang 
             << setw(15) << strNgay 
             << setw(20) << fixed << setprecision(2) << a[i].giaXuat << endl;
    }
}

void SelectionSort(HangHoa a[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (a[j].giaXuat < a[minIdx].giaXuat) {
                minIdx = j;
            }
        }
        if (minIdx != i) {
            HangHoa tmp = a[i];
            a[i] = a[minIdx];
            a[minIdx] = tmp;
        }
    }
}

void timKiemNhiPhan(HangHoa a[], int n, double x) {
    int left = 0, right = n - 1;
    bool found = false;
    
    while (left <= right) {
        int mid = (left + right) / 2;
        if (a[mid].giaXuat == x) {
            found = true;
            int i = mid;
            while (i >= 0 && a[i].giaXuat == x) i--;
            int j = mid;
            while (j < n && a[j].giaXuat == x) j++;
            
            cout << "\nCac hang hoa co gia xuat bằng " << x << " trieu dong la:\n";
            cout << left << setw(15) << "Ma Hang" 
                 << setw(25) << "Ten Hang" 
                 << setw(15) << "Ngay Xuat" 
                 << setw(20) << "Gia Xuat (Trieu)" << endl;
            cout << string(75, '-') << endl;
            for (int k = i + 1; k < j; k++) {
                string strNgay = to_string(a[k].ngayXuat.ngay) + "/" + 
                                 to_string(a[k].ngayXuat.thang) + "/" + 
                                 to_string(a[k].ngayXuat.nam);
                cout << left << setw(15) << a[k].maHang 
                     << setw(25) << a[k].tenHang 
                     << setw(15) << strNgay 
                     << setw(20) << fixed << setprecision(2) << a[k].giaXuat << endl;
            }
            break;
        }
        if (a[mid].giaXuat < x)
            left = mid + 1;
        else
            right = mid - 1;
    }
    if (!found) {
        cout << "\nKhong tim thay hang hoa nao co gia xuat bang " << x << " trieu dong.\n";
    }
}

int main() {
    int n;
    cout << "Nhap so luong hang hoa: ";
    cin >> n;

    if (n <= 0) return 0;

    HangHoa a[100];
    
    nhapDanhSach(a, n);
    
    cout << "\nDANH SACH HANG HOA VUA NHAP:\n";
    xuatDanhSach(a, n);
    
    SelectionSort(a, n);
    cout << "\nDANH SACH SAU KHI SAP XEP TANG DAN THEO GIA XUAT:\n";
    xuatDanhSach(a, n);
    
    double x;
    cout << "\nNhap gia xuat X can tim: ";
    cin >> x;
    timKiemNhiPhan(a, n, x);
    
    return 0;
}
