<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Merge Sort with User Input</title>
</head>
<body>
    <pre>
#include &lt;iostream&gt;
#include &lt;vector&gt;
using namespace std;

void Merge(vector&lt;int&gt;& B, vector&lt;int&gt;& C, vector&lt;int&gt;& A) {
    int p = B.size();
    int q = C.size();
    int i = 0;
    int j = 0;
    int k = 0;

    while (i &lt; p && j &lt; q) {
        if (B[i] &lt;= C[j]) {
            A[k] = B[i];
            i = i + 1;
        } else {
            A[k] = C[j];
            j = j + 1;

        }
        k = k + 1;
    }

    if (i == p) {
        while (j &lt; q) {
            A[k] = C[j];
            j = j + 1;
            k = k + 1;
        }
    } else {
        while (i &lt; p) {
            A[k] = B[i];
            i = i + 1;
            k = k + 1;
        }
    }
}

void MergeSort(vector&lt;int&gt;& A) {
    int n = A.size();
    if (n &gt; 1) {
        int mid = n / 2;

        vector&lt;int&gt; B(mid);
        vector&lt;int&gt; C(n - mid);

        for (int i = 0; i &lt; mid; i++) {
            B[i] = A[i];
        }
        for (int i = mid; i &lt; n; i++) {
            C[i - mid] = A[i];
        }

        MergeSort(B);
        MergeSort(C);
        Merge(B, C, A);
    }
}

int main() {
    int n;
    cout &lt;&lt; "Enter the number of elements: ";
    cin &gt;&gt; n;

    vector&lt;int&gt; A(n);
    cout &lt;&lt; "Enter the elements:" &lt;&lt; endl;
    for (int i = 0; i &lt; n; i++) {
        cin &gt;&gt; A[i];
    }

    MergeSort(A);

    cout &lt;&lt; "Sorted elements: ";
    for (int i = 0; i &lt; A.size(); i++) {
        cout &lt;&lt; A[i] &lt;&lt; " ";
    }

    return 0;
}
    </pre>
</body>
</html>
