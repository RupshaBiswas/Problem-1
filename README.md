#include <stdio.h>
#include <string.h>

int main() {
    char s[100005];
    scanf("%s", s);

    int n = strlen(s);

    
    char t[200010];
    strcpy(t, s);
    strcat(t, s);

    int last[26];
    for (int i = 0; i < 26; i++)
        last[i] = -1;

    int left = 0;
    int currSum = 0;
    int maxSum = 0;

    for (int right = 0; right < 2 * n; right++) {

        int ch = t[right] - 'a';

        // Remove characters until window is valid
        while (last[ch] >= left || (right - left + 1) > n) {
            currSum -= (t[left] - 'a' + 1);
            left++;
        }

        currSum += (ch + 1);
        last[ch] = right;

        if (currSum > maxSum)
            maxSum = currSum;
    }

    printf("%d\n", maxSum);

    return 0;
}
