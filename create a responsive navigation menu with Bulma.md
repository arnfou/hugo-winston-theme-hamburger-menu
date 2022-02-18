Download bulma.min.css from Bulma CSS framework
  See https://cdnjs.cloudflare.com/ajax/libs/bulma/0.7.4/css/bulma.min.css
  See https://pakstech.com/blog/create-theme-layout/

Open the file and look for:
  Find "Segoe UI" (default font from Bulma theme)
  Replace by "Poppins" (default font from the Winston theme)

  Find "3273dc" (default highlight color from Bulma theme)
  Replace by "7b16ff" (default highligh color from Winston theme)

Add bulma.min.css in /static/css

Open /themes/hugo-winston-theme/layouts/_partials/header.html and add the following lines
  <link rel="stylesheet" href="{{ absURL "/css/bulma.min.css" }}">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

  Remove
  <a class="header-logo" href="{{ .Site.BaseURL }}">{{ .Site.Title }}</a>
  <div class="menu-main">
    <ul>
        {{ $currentPage := . }}
        {{ range .Site.Menus.main }}
            <li class="menu-item-{{ .Name | lower }}{{ if $currentPage.IsMenuCurrent "main" . }} active{{ end }}">
                <a href="{{ .URL | relLangURL }}">{{ .Name }}</a>
            </li>
        {{end}}
    </ul>
  </div>

  And replace by:
  <nav class="navbar" role="navigation">
       <div class="container">
           <div class="navbar-brand">
               <a href="/" title="home" class="navbar-item">
                   <span class="header-logo"><h1>{{ .Site.Title }}</h1></span>
               </a>
               {{ range .Site.Menus.social }}
               <a href="{{ .URL }}" class="navbar-item is-hidden-desktop" title="{{ .Name }}"><span
                       class="icon">{{ .Pre }}</span></a>
               {{ end }}
               <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
                   <span aria-hidden="true"></span>
                   <span aria-hidden="true"></span>
                   <span aria-hidden="true"></span>
               </a>
           </div>
           <div class="navbar-menu">
               <div class="navbar-start">
                   {{ range .Site.Menus.main }}
                   <a href="{{ .URL }}" class="navbar-item">{{ .Name }}</a>
                   {{ end }}
               </div>
               <div class="navbar-end">
                   {{ range .Site.Menus.social }}
                   <a href="{{ .URL }}" class="navbar-item is-hidden-touch" title="{{ .Name }}"><span
                           class="icon">{{ .Pre }}</span></a>
                   {{ end }}
               </div>
           </div>
       </div>
   </nav>
   <script>
       $(document).ready(function () {
           $(".navbar-burger").click(function () {
               $(".navbar-burger").toggleClass("is-active");
               $(".navbar-menu").toggleClass("is-active");
           })
       })
   </script>

Go to config.toml and add:

[[menu.main]]
  name = "Home"
  url = "/"

[[menu.main]]
  name = "Posts"
  url = "/posts"

[[menu.main]]
  name = "About"
  url = "/pages/about"
