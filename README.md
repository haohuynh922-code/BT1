# BT1
#include <iostream>
using namespace std;

const int MAX = 100;
int m, n;
int a[MAX][MAX];
int Duyet[MAX][MAX];
int queueX[MAX * MAX], queueY[MAX * MAX], dist[MAX * MAX];

int dx[] = { 0, 1, 0, -1 }; 
int dy[] = { 1, 0, -1, 0 };

void nhap() {
    cout << "Nhap so hang (m): ";
    cin >> m;
    cout << "Nhap so cot (n): ";
    cin >> n;

    cout << "\nNhap ma tran ban do (" << m << "x" << n << "):\n";
    cout << "(0: duong di, -1: vat can)\n";
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            cin >> a[i][j];
        }
    }
}

void xuat() {
    cout << "\nBan do kho hang:\n";
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (a[i][j] == -1) cout << " I "; 
            else cout << " O "; 
        }
        cout << endl;
    }
}

int bfs(int sx, int sy, int ex, int ey) {
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            Duyet[i][j] = 0;

    int front = 0, rear = 0;
    queueX[rear] = sx;
    queueY[rear] = sy;
    dist[rear] = 0;
    Duyet[sx][sy] = 1;
    rear++;

    while (front < rear) {
        int x = queueX[front];
        int y = queueY[front];
        int d = dist[front];
        front++;

        if (x == ex && y == ey) return d;

        for (int i = 0; i < 4; ++i) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx >= 0 && ny >= 0 && nx < m && ny < n &&
                a[nx][ny] != -1 && !Duyet[nx][ny]) {
                Duyet[nx][ny] = 1;
                queueX[rear] = nx;
                queueY[rear] = ny;
                dist[rear] = d + 1;
                rear++;
            }
        }
    }
    return -1; 
}

int main() {
    nhap();
    xuat();

    int startX, startY, endX, endY;
    cout << "\nNhap toa do diem bat dau [(hang-1) (cot-1)]: ";
    cin >> startX >> startY;
    cout << "Nhap toa do diem ket thuc [(hang-1) (cot-1)]: ";
    cin >> endX >> endY;

    int result = bfs(startX, startY, endX, endY);
    if (result != -1)
        cout << "\nDuong di ngan nhat: " << result << " buoc.\n";
    else
        cout << "\nKhong tim thay duong di!\n";

    return 0;
}
