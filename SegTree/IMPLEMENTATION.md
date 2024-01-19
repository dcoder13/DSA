

```C++
template <typename T>
class segtree{
    private:
        int sizee;
        vector<T> tree;
        void init(int n){
            sizee = 1;
            while(sizee < n) sizee *= 2;
            tree.resize(2*sizee-1, 0);
        }
        T operation(T a, T b)
        {
            return a + b;
        }
        void build(vector<T> &a, int x, int lx, int rx){
            if(rx - lx == 1){
                if(lx < (int)a.size()){
                    tree[x] = a[lx];
                }
                return;
            }
            int m = (lx + rx)/2;
            build(a, 2*x+1, lx, m);
            build(a, 2*x+2, m, rx);
            tree[x] = operation(tree[2*x+1], tree[2*x+2]);
        }
        T get(int l, int r, int x, int lx, int rx){
            if(lx >= r || l >= rx) return 0;
            if(lx >= l && rx <= r) return tree[x];
            int m = (lx + rx)/2;
            T s1 = get(l, r, 2*x+1, lx, m);
            T s2 = get(l, r, 2*x+2, m, rx);
            return operation(s1, s2);
        }
        void set(int i, int x, int lx, int rx, T v){
            if(rx - lx == 1){
                tree[x] = v;
                return;
            }
            int m = (lx + rx)/2;
            if(i < m){
                set(i, 2*x+1, lx, m, v);
            }
            else{
                set(i, 2*x+2, m, rx, v);
            }
            tree[x] = operation(tree[2*x+1], tree[2*x+2]);
        }
    public:
        segtree(int n){
            init(n);
        }
        segtree(int n, vector<T> a){
            init(n);
            build(a, 0, 0, sizee);
        }
        int size(){
            return sizee;
        }
        // L to R-1
        T get(int l, int r){ 
            return get(l, r, 0, 0, sizee);
        }
        void set(int i, T v){
            set(i, 0, 0, sizee, v);
        }
        // operator overloading
        segtree operator=(segtree &other){
            size = other.size;
            tree = other.tree;
            return *this;
        }
        T operator[](int i){
            return tree[i];
        }
};
```
