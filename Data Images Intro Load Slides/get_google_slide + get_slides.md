def get_google_slide(url):
    # Construct the Google Slides URL
    url_head = "https://docs.google.com/presentation/d/"
    url_body = url.split('/')[5]
    page_id = url.split('.')[-1]
    return url_head + url_body + "/export/pdf?id=" + url_body + "&pageid=" + page_id

def get_slides(url):
    # Get the PDF from Google Slides
    url = get_google_slide(url)
    r = requests.get(url, allow_redirects=True)
    open('file.pdf', 'wb').write(r.content)
    
    # Convert PDF to images
    images = convert_from_path('file.pdf', 500)
    return images
