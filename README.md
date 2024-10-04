# autoStattic - import content from your WordPress site

A Python script to fetch WordPress posts, pages, authors, categories, tags, and custom taxonomies via the WordPress REST API and convert them into Markdown files with YAML front matter. Ideal for migrating content to static site generators or other Markdown-based workflows.

## Features

- **Content Fetching**: Retrieves posts, pages, authors, categories, tags, and custom taxonomies from a WordPress site.
- **Markdown Conversion**: Converts WordPress content to Markdown, preserving metadata through YAML front matter.
- **HTML Handling**: Options to convert HTML content to Markdown or preserve complex HTML blocks (like Gutenberg blocks).
- **Media Link Processing**: Adjusts media links to point to local versions.
- **Custom Taxonomies**: Automatically detects and processes custom taxonomies.
- **Command-Line Interface**: Flexible options provided via command-line arguments.

## Requirements

- Python 3.x
- Packages:
    - `requests`
    - `PyYAML`
    - `html2text`
    - `tqdm`

Install the required packages using:
    
    pip install -r requirements.txt
    

## Installation

1. **Clone the Repository**
    
    git clone https://github.com/yourusername/your-repository.git
    cd your-repository
    

2. **Install Dependencies**
    
    pip install -r requirements.txt
    

## Usage
    
    python wordpress_to_markdown.py [options] <WordPress_Site_URL>
    

### Positional Arguments

- `<WordPress_Site_URL>`: The base URL of your WordPress site (e.g., `https://your-site.com`).

### Optional Arguments

- `--markdown`: Convert HTML content to Markdown using `html2text`. Without this flag, the script preserves complex HTML blocks.

### Examples

- **Preserve HTML Blocks**
    
    python wordpress_to_markdown.py https://your-site.com
    
- **Convert HTML to Markdown**
    
    python wordpress_to_markdown.py https://your-site.com --markdown

## Output

The script generates a `content` directory with the following structure:

- `content/posts/`: Markdown files for each post.
- `content/pages/`: Markdown files for each page.
- `content/authors.yml`: YAML file mapping author IDs to names.
- `content/categories.yml`: YAML file containing category data.
- `content/tags.yml`: YAML file containing tag data.

Each Markdown file includes YAML front matter with metadata:

- `title`
- `date`
- `author`
- `excerpt`
- `custom_url`
- `type` (post or page)
- `categories`
- `tags`
- Custom taxonomies (if any)
- Advanced Custom Fields (ACF) data (if available)

## Configuration

- **Content Directory**: Modify the `CONTENT_DIR` variable in the script to change the output directory.
- **HTML to Markdown Conversion Settings**: Adjust the `html_converter` settings to fine-tune Markdown conversion.
- **API Pagination**: Change the `per_page` parameter in `fetch_wordpress_data()` to adjust items fetched per API call.

## Handling Custom Taxonomies

The script automatically detects custom taxonomies and processes them accordingly. Custom taxonomy terms are included in the YAML front matter of each Markdown file.

## Limitations

- **Authentication**: The script does not support authenticated endpoints. It works with publicly accessible WordPress REST APIs.
- **Media Files**: While media links are processed, actual media files (images, attachments) are not downloaded.
- **Error Handling**: The script includes basic error handling, but unexpected API responses may cause issues.

## Troubleshooting

- **HTTP Errors**: Ensure the WordPress REST API is accessible at `https://your-site.com/wp-json/wp/v2/`.
- **Empty Responses**: Check if the site has content and that the correct endpoints are being accessed.
- **Invalid JSON Responses**: Verify that the API responses are valid JSON. Issues may arise due to plugins or themes interfering with API output.

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests for improvements or bug fixes.
