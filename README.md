#ktra1909
#include <stdio.h>
#include <string.h>
#define MAX 100
struct hanghoa{
    char mahh[10];
    char tenhh[50];
    int ngay, thang, nam;
    float giaxuat;
};
void nhapmang(struct hanghoa a[], int n){
    for (int i = 0; i < n; i++){
        printf("\nnhap hang hoa thu %d:\n", i + 1);
        printf("ma hang hoa: ");
        fflush(stdin);
        gets(a[i].mahh);
        printf("ten hang hoa: ");
        fflush(stdin);
        gets(a[i].tenhh);
        printf("ngay xuat hang (nn tt nnnn): ");
        scanf("%d %d %d", &a[i].ngay, &a[i].thang, &a[i].nam);
        printf("gia xuat hang: ");
        scanf("%f", &a[i].giaxuat);
    }
}
void inmang(struct hanghoa a[], int n){
    printf("\n%-10s%-20s%-15s%-10s\n", "ma hh", "ten hh", "ngay xuat", "gia xuat");
    for (int i = 0; i < n; i++)
    {
        printf("%-10s%-20s%02d/%02d/%04d     %.2f\n",
        a[i].mahh, a[i].tenhh, a[i].ngay, a[i].thang, a[i].nam, a[i].giaxuat);
    }
}
void xapxep(struct hanghoa a[], int n){
    for (int i = 0; i < n - 1; i++){
        int min = i;
        for (int j = i + 1; j < n; j++){
            if (a[j].giaxuat < a[min].giaxuat)
                min = j;
        }
        if (min != i){
            struct hanghoa tam = a[i];
            a[i] = a[min];
            a[min] = tam;
        }
    }
}
int nhiphan(struct hanghoa a[], int n, float x){
    int dau = 0, cuoi = n - 1;
    while (dau <= cuoi){
        int giua = (dau + cuoi) / 2;
        if (a[giua].giaxuat == x)
            return giua;
        else if (a[giua].giaxuat < x)
            dau = giua + 1;
        else
            cuoi = giua - 1;
    }
    return -1;
}

void tim(struct hanghoa a[], int n, float x){
    int vt = nhiphan(a, n, x);
    if (vt == -1){
        printf("\nkhong tim thay hang hoa nao co gia xuat = %.2f\n", x);
        return;
    }
    int trai = vt, phai = vt;
    while (trai - 1 >= 0 && a[trai - 1].giaxuat == x)
        trai--;
    while (phai + 1 <= n - 1 && a[phai + 1].giaxuat == x)
        phai++;
    printf("\ncac hang hoa co gia xuat = %.2f:\n", x);
    printf("%-10s%-20s%-15s%-10s\n", "ma hh", "ten hh", "ngay xuat", "gia xuat");
    for (int i = trai; i <= phai; i++){
        printf("%-10s%-20s%02d/%02d/%04d     %.2f\n",
               a[i].mahh, a[i].tenhh, a[i].ngay, a[i].thang, a[i].nam, a[i].giaxuat);
    }
}
int main(){
    struct hanghoa a[MAX];
    int n;
    float x;
    printf("nhap so luong hang hoa : ");
    scanf("%d", &n);
    nhapmang(a, n);
    printf("\ndanh sach hang hoa vua nhap:");
    inmang(a, n);
    xapxep(a, n);
    printf("\ndanh sach hang hoa sau khi sap xep theo gia xuat tang dan:");
    inmang(a, n);
    printf("\nnhap gia xuat can tim X: ");
    scanf("%f", &x);
    tim(a, n, x);
    return 0;
}
