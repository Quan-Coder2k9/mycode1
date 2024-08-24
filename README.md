#include <bits/stdc++.h>
using namespace std;
const int maxN = 5 * 1e4 + 3;  
int a[maxN];
int st[4 * maxN];
int n,m,x,y,z,type;
/*void build(int id, int l, int r) {
	if (l == r) {
		st[id] = a[l];
		return;
	}
	mid = l + r >> 1;
	build(2 * id, l, mid);
	build(2 * id + 1, mid + 1, r);
	st[id] = max(st[2 * id], st[2 * id + 1]);
}*/
void update(int id, int l, int r,int u, int v, int val) {
	if (l > v || r < u) return;
	if (l == r) {
		st[id] += val;
		return;
	}
	int mid = l + r >> 1;
	update(2 * id, l, mid, u, v, val);
	update(2 * id + 1, mid + 1, r, u, v, val);
	st[id] = max(st[2 * id], st[2 * id + 1]);
}
int get(int id, int l, int r, int u, int v) {
	if (l > v || r < u) return 0;
	if (l >= u && r <= v) return st[id];
	int mid = l + r >> 1;
	int get1 = get(2 * id, l, mid, u, v);
	int get2 = get(2 * id + 1, mid + 1, r, u, v);
	return max(get1, get2);
}
int main() {
	ios_base::sync_with_stdio(0); 
    cin.tie(0); 
	cin >> n >> m;
	for (int i = 1; i <= m; i++) {
		cin >> type;
		if (type) {
			cin >> x >> y;
			cout << get(1,1,n,x,y) << '\n';
		}
		else {
			cin >> x >> y >> z;
			update(1,1,n,x,y,z);
		}
	}
}
