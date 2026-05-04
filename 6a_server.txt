from flask import Flask, render_template, request 
from EmotionDetection.emotion_detection import emotion_detector

app = Flask("Emotion Detector")

@app.route("/") 
def render_index_page(): 
    return render_template('index.html')

@app.route("/emotionDetector") 
def sent_analyzer(): 
    text_to_analyze = request.args.get('textToAnalyze')

    response = emotion_detector(text_to_analyze)
 
    anger = response['anger']
    disgust = response['disgust']
    fear = response['fear']
    joy = response['joy']
    sadness = response['sadness']
    dominant = response['dominant_emotion']

    formatted_response = (
        f"For the given statement, the system response is 'anger': {anger}, 'disgust': {disgust}, 'fear': {fear}, 'joy': {joy} and 'sadness': {sadness}. "
        f"The dominant emotion is {dominant}."
    )

    return formatted_response

if __name__ == "__main__":
    app.run(debug=True)