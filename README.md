# word_count
search a word count
#include <stdio.h>

#include <string.h>
#include <ctype.h>


void to_lowercase(char *str)
{
    for (int i = 0; str[i]; i++)
    {
        str[i] = tolower(str[i]);
    }
}

int main()
{
    FILE *file;
    char paragraph[10000]; 
    char word[100];        
    char myfile[] = "myfile.txt";
    int count = 0;

    
    file = fopen(myfile, "r");
    if (file == NULL)
    {
        printf("Error opening file %s\n", myfile);
        return 1;
    }

    
    fread(paragraph, sizeof(char), sizeof(paragraph) - 1, file);
    paragraph[sizeof(paragraph) - 1] = '\0'; 
    fclose(file);

    
    to_lowercase(paragraph);

    
    printf("Enter the word to search: ");
    scanf("%s", word);
    to_lowercase(word); 

    
    char *token = strtok(paragraph, " \n\t,.!?;:\"()[]{}");
    while (token != NULL)
    {
        if (strcmp(token, word) == 0)
        {
            count++;
        }
        token = strtok(NULL, " \n\t,.!?;:\"()[]{}");
    }

    printf("The word '%s' appears %d time(s) in the paragraph.\n", word, count);

    return 0;
}
