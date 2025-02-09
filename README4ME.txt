If I miss some _() or _l() from Babel translations, I update the code and then update messages.pot with the following
command to keep everything up to date.

(venv) $ pybabel extract -F babel.cfg -k _l -o messages.pot .
(venv) $ pybabel update -i messages.pot -d app/
(Don't forget to:)
(venv) $ pybabel compile -d app/translations