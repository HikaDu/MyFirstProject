# MyFirstProject
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>


struct Paper
{
    int id;
    std::string title;
    std::string content;
};


std::vector<Paper> searchPapers(const std::vector<Paper>& papers, const std::string& query)
{
    std::vector<Paper> results;

    for (const Paper& paper : papers)
    {
        std::string lowerTitle = paper.title;
        std::transform(lowerTitle.begin(), lowerTitle.end(), lowerTitle.begin(), ::tolower);
        std::string lowerContent = paper.content;
        std::transform(lowerContent.begin(), lowerContent.end(), lowerContent.begin(), ::tolower);

        if (lowerTitle.find(query) != std::string::npos || lowerContent.find(query) != std::string::npos)
        {
            results.push_back(paper);
        }
    }

    return results;
}

int main()
{
    // Sample academic papers
    std::vector<Paper> papers =
    {
        {1, "Title 1", "This paper discusses algorithms in computer science."},
        {2, "Title 2", "C++ programming language is powerful and widely used."},
        {3, "Title 3", "Machine learning techniques are widely used in various applications."},
        {4, "Title 4", "The importance of data structures in computer science."},
        {5, "Title 5", "Linear search is a basic search algorithm."},
    };

    // Ask the user for a search query
    std::cout << "Enter your search query: ";
    std::string query;
    std::getline(std::cin, query);

    // Perform the search
    std::vector<Paper> searchResults = searchPapers(papers, query);

    // Display the search results
    if (searchResults.empty())
    {
        std::cout << "No matching papers found." << std::endl;
    }
    else
    {
        std::cout << "Matching papers:" << std::endl;
        for (const Paper& paper : searchResults)
        {
            std::cout << "[" << paper.id << "] " << paper.title << std::endl;
        }
    }

    return 0;
}
