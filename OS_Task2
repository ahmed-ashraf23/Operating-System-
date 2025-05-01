#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void FCFS(int queue[], int size, int head) {
    int total_seek = 0;
    printf("\nFCFS Order: %d", head);
    for (int i = 0; i < size; i++) {
        total_seek += abs(queue[i] - head);
        printf(" -> %d", queue[i]);
        head = queue[i];
    }
    printf("\nTotal Seek Time: %d\n", total_seek);
}

void SCAN(int queue[], int size, int head, int max_cylinders) {
    int total_seek = 0;
    int left[size], right[size];
    int l = 0, r = 0;

    for (int i = 0; i < size; i++) {
        if (queue[i] < head) left[l++] = queue[i];
        else right[r++] = queue[i];
    }

    // sort left descending
    for (int i = 0; i < l - 1; i++)
        for (int j = i + 1; j < l; j++)
            if (left[i] < left[j]) {
                int temp = left[i];
                left[i] = left[j];
                left[j] = temp;
            }

    // sort right ascending
    for (int i = 0; i < r - 1; i++)
        for (int j = i + 1; j < r; j++)
            if (right[i] > right[j]) {
                int temp = right[i];
                right[i] = right[j];
                right[j] = temp;
            }

    printf("\nSCAN Order: %d", head);

    for (int i = 0; i < l; i++) {
        total_seek += abs(left[i] - head);
        printf(" -> %d", left[i]);
        head = left[i];
    }

    if (l > 0) {
        total_seek += head;
        printf(" -> 0");
        head = 0;
    }

    for (int i = 0; i < r; i++) {
        total_seek += abs(right[i] - head);
        printf(" -> %d", right[i]);
        head = right[i];
    }

    printf("\nTotal Seek Time: %d\n", total_seek);
}

void C_SCAN(int queue[], int size, int head, int max_cylinders) {
    int total_seek = 0;
    int left[size], right[size];
    int l = 0, r = 0;

    for (int i = 0; i < size; i++) {
        if (queue[i] < head) left[l++] = queue[i];
        else right[r++] = queue[i];
    }

    // sort left ascending
    for (int i = 0; i < l - 1; i++)
        for (int j = i + 1; j < l; j++)
            if (left[i] > left[j]) {
                int temp = left[i];
                left[i] = left[j];
                left[j] = temp;
            }

    // sort right ascending
    for (int i = 0; i < r - 1; i++)
        for (int j = i + 1; j < r; j++)
            if (right[i] > right[j]) {
                int temp = right[i];
                right[i] = right[j];
                right[j] = temp;
            }

    printf("\nC-SCAN Order: %d", head);

    for (int i = 0; i < r; i++) {
        total_seek += abs(right[i] - head);
        printf(" -> %d", right[i]);
        head = right[i];
    }

    if (r > 0) {
        total_seek += (max_cylinders - 1 - head);
        printf(" -> %d", max_cylinders - 1);
        total_seek += (max_cylinders - 1);
        printf(" -> 0");
        head = 0;
    }

    for (int i = 0; i < l; i++) {
        total_seek += abs(left[i] - head);
        printf(" -> %d", left[i]);
        head = left[i];
    }

    printf("\nTotal Seek Time: %d\n", total_seek);
}

int main() {
    int queue_size, initial, max_cylinders;
    char algorithm[20];
    char choice[10];
    int first_run = 1;

    while (1) {
        if (first_run || strcmp(choice, "START") == 0) {
            printf("Enter Queue Size: ");
            scanf("%d", &queue_size);
        }

        int queue[queue_size];

        printf("Enter the Requests: ");
        for (int i = 0; i < queue_size; i++) {
            scanf("%d", &queue[i]);
        }

        if (first_run || strcmp(choice, "START") == 0) {
            printf("Enter Initial Position: ");
            scanf("%d", &initial);

            printf("Enter Number of Cylinders: ");
            scanf("%d", &max_cylinders);
        }

        printf("Enter Algorithm (FCFS / SCAN / C-SCAN / ALL): ");
        scanf("%s", algorithm);

        // Convert to uppercase
        for (int i = 0; algorithm[i]; i++) {
            if (algorithm[i] >= 'a' && algorithm[i] <= 'z') {
                algorithm[i] -= 32;
            }
        }

        if (strcmp(algorithm, "FCFS") == 0) {
            FCFS(queue, queue_size, initial);
        } else if (strcmp(algorithm, "SCAN") == 0) {
            SCAN(queue, queue_size, initial, max_cylinders);
        } else if (strcmp(algorithm, "C-SCAN") == 0 || strcmp(algorithm, "C_SCAN") == 0) {
            C_SCAN(queue, queue_size, initial, max_cylinders);
        } else if (strcmp(algorithm, "ALL") == 0) {
            FCFS(queue, queue_size, initial);
            SCAN(queue, queue_size, initial, max_cylinders);
            C_SCAN(queue, queue_size, initial, max_cylinders);
        } else {
            printf("Invalid algorithm name.\n");
        }

        printf("\nEnter 'START' to run again, 'CONTINUE' to reuse previous settings, or 'EXIT' to quit: ");
        scanf("%s", choice);

        // Convert to uppercase
        for (int i = 0; choice[i]; i++) {
            if (choice[i] >= 'a' && choice[i] <= 'z') {
                choice[i] -= 32;
            }
        }

        if (strcmp(choice, "EXIT") == 0) {
            printf("Exiting the program.\n");
            break;
        } else if (strcmp(choice, "START") != 0 && strcmp(choice, "CONTINUE") != 0) {
            printf("Invalid choice. Exiting by default.\n");
            break;
        }

        first_run = 0;
    }

    return 0;
}
