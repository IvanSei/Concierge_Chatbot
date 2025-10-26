Der Hotel Concierge Chatbot ist ein KI-gestützter Chatbot, der speziell für das Hotel Les Trois Rois in Basel entwickelt wurde. Er soll Hotelgästen rund um die Uhr bei allgemeinen Fragen weiterhelfen. Zum Beispiel zu den angebotenen Dienstleistungen, Sehenswürdigkeiten in Basel oder zur Orientierung in der Stadt. Der Chatbot kann auch Auskünfte zu nahegelegenen Grossstädten wie Zürich oder Paris geben, die direkt mit der SBB erreichbar sind.
Technisch basiert das Projekt auf einem RAG. Das bedeutet, dass der Chatbot seine Antworten nicht nur aus einem trainierten Sprachmodell generiert, sondern zusätzlich auf externe Quellen wie Hotelinformationen oder PDF-Dokumente mit relevanten Informationen zugreift. Dadurch kann er präzisere und aktuellere Antworten liefern, die zum Kontext des Hotels und der Umgebung passen.


#Problemstellung

Wir haben diesen Use Case ausgewählt, weil wir alle von unserer Gruppe schon eimal in mindestens einem Hotel gewesen sind und festgestellt haben, dass es am Empfang meistens keinen Chatbot hatte. Wenn keine Person anwesend war, ergaben sich folgende Situationen:
Situation 1: Eine Person kommt ins Hotel und es ist niemand da. Am Schalter steht entweder ein Schild mit der Aufschrift: „Es wird gleich jemand für Sie da sein“ oder ein Schild mit einer ähnlichen Formulierung wie „Der Concierge/die Rezeptionistin ist gerade abwesend. Rufen Sie unter folgender Nummer an, dann wird gleich jemand für Sie da sein“.
Situation 2: Eine Person kommt ins Hotel, aber es ist niemand da und auch keine weiteren Informationen zur Verfügung. Nur die Zeiten, in denen das Hotel betreut ist, sind bekannt. Das kann in kleinen Hotels mit weniger Sternen vorkommen.
In beiden Situationen müssen die Hotelgäste warten. Und da kommen wir mit unserem Hotel Concierge Chatbot ins Spiel, der die Wartezeit überbrückt und die gängigsten Fragen beantworten kann. So erhalten die Gäste Antworten auf ihre Fragen und haben etwas mehr Geduld, bis der Concierge zurückgekehrt ist.
Auch bereits eingecheckte Gäste profitieren von dem Chatbot. Wenn sie zum Beispiel schon vor Ort sind und die Stadt erkunden möchten, aber noch nicht wissen wohin, können sie den Chatbot fragen. Er wird ihnen auch diese Frage beantworten können.


Anleitung

Lade das Projekt herunter oder oder kreiere eine lokale Version mit git clone <repository-url>
Wichtig ist zu beachten, dass ihr im richtigen Dateipfad, also am richtigen Speicherort seid, damit das Progamm ausgeführt werden kann. Achtet bitte, dass ihr dort sein müsst, wo die Ordner wie app, data, docs… drinnen sind. Im Terminal gebt ihr ein: cd <und dann euren Dateipfad zum Chatbot>. 

Jetzt muss eine .env Datei erstellt werden. Sie wird dort abgespeichert, wo die LICENSE und README.md ist

Die .env Datei im Projekt hat folgenden Code:
LANGCHAIN_TRACING_V2=true
LANGCHAIN_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=<your_langsmith_key>
LANGSMITH_PROJECT=Hotel-Concierge-RAG
CEREBRAS_API_KEY=<your_cerebras_key>
CEREBRAS_API_BASE=https://api.cerebras.ai/v1
MODEL_NAME=llama-3.1-8b
USER_AGENT=hotel-concierge-bot/1.0
#OPENAI_API_KEY=<optional>
OPENAI_BASE_URL=https://api.cerebras.ai/v1
GRADIO_SERVER_PORT=7860
EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2
CHUNK_SIZE=700
CHUNK_OVERLAP=120
TOP_K=4
HOTEL_NAME=Trois Rois

Wichtig ist, hier die API Keys einzufügen. Zum Beispiel den Cerebras API Key bei CEREBRAS_API_KEY.
Die persönlichen Dateien mit den eigenen API-Keys nie auf Github pushen.

Dann Requirements auch am gleichen Speicherort wie die .env Datei mit folgendem Code einfügen:
langchain==0.3.7
langchain-core==0.3.20
langchain-community==0.3.7
langchain-openai==0.2.6
openai==1.109.1
python-dotenv==1.0.1
tiktoken==0.12.0
faiss-cpu==1.8.0.post1
sentence-transformers==3.2.1
pypdf==5.0.0
beautifulsoup4==4.12.3
lxml==5.3.0
html2text==2024.2.26
requests==2.32.5
gradio==5.49.1
chromadb==1.2.0
langfuse==2.40.0
rank-bm25==0.2.2



Danach ist es wichtig auf ‘Edit Configurations’ zu klicken und unter app die Datei ‘ui.py’ auswählen. Das ist der richtige Dateipfad.
<img width="945" height="601" alt="image" src="https://github.com/user-attachments/assets/845d8f4f-2cc1-4dfb-ba18-9427dd1fdc45" />


Als nächstes das Terminal öffnen.
Venv aktivieren:
Windows:	.venv\Scripts\activate
Mac/Linux:	source .venv/bin/activate
Das erste Mal, müssen die requirements installiert werden
pip install -r requirements.txt

(Nur wenn langchain eine falsche Meldung herausgibt: 
pip uninstall -y langchain_huggingface)

Danach:
python -m app.ui
Es zeigt, wenn alles funktioniert hat, im Terminal den Link http://0.0.0.0:7860 an. Diesen Link anklicken, um zum Chatbot zu gelangen. Sollte der Link nicht funktionieren, einfach im Browser localhost:7860 in der oberen Suchleiste eingeben.




