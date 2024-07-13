# Generating documentation site
These instructions are done with windows WSL2 under ubuntu 22.04 LTS


## setup mkdocs in your environment
Install the python packages
```sh
pip install mkdocs
pip install mkdocs-material
pip install mkdocs-material[imaging]
```

Test to see everything working
```sh
mkdocs build
mkdocs serve
mkdocs gh-deploy
```

Install pandoc on your OS
```sh
apt install pandoc
apt install texlive texlive-latex-extra texlive-latex-recommended texlive-xetex
```
Verify Pandoc installed properly
```sh
pandoc --help
```

Install the python package, mind the name there are different ones floating around
https://pypi.org/project/mkdocs-pandoc-plugin/

```sh
pip install mkdocs-pandoc-plugin
```

Add pandoc in the plugin section of mkdocs.yml
```
plugins:
    - search
    - pandoc:
        combined: True
```
Note: If you have no plugins entry in your config file yet, you'll likely also want to add the search plugin.
MkDocs enables it by default if there is no plugins entry set, but now you have to enable it explicitly.

Running the build command you probqbly still get errors
```sh
mkdocs build --verbose
```

Replace offending characters
```sh
sed -i "s/├/|-/g" docs/how-to/Start-a-New-CrewAI-Project.md 
sed -i "s/─/-/g" docs/how-to/Start-a-New-CrewAI-Project.md 
sed -i "s/└/+/g" docs/how-to/Start-a-New-CrewAI-Project.md 
sed -i "s/│/|/g" docs/how-to/Start-a-New-CrewAI-Project.md 
```
Starting replace more offending characters but gave up for now
```sh
sed -i "s/🐦/X/g" docs/how-to/AgentOps-Observability.md 
sed -i "s/📢/mkdocs build --verbose/g" docs/how-to/AgentOps-Observability.md 
sed -i "s/📢/ll/g" docs/how-to/AgentOps-Observability.md 
sed -i "s/🖇/DB/g" docs/how-to/AgentOps-Observability.md 
mv docs/how-to/AgentOps-Observability.md docs/how-to/AgentOps-Observability.md_utf
```

```sh
mkdocs build --verbose
ls -l site/pandoc
mkdocs gh-deploy
```

Done, Enjoy the file in your local director and/or published on github pages
