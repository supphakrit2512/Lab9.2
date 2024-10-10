# Lab9.2

from flask import Flask, render_template_string
 
app = Flask(__name__)
 
# สถานะของหลอด LED
led_status = {
    'led1': 'OFF',
    'led2': 'OFF'
}
 
@app.route('/')
def index():
    return render_status()
 
@app.route('/led1/<state>')
def led1(state):
    if state == 'on':
        led_status['led1'] = 'ON'
    elif state == 'off':
        led_status['led1'] = 'OFF'
    return render_status()
 
@app.route('/led2/<state>')
def led2(state):
    if state == 'on':
        led_status['led2'] = 'ON'
    elif state == 'off':
        led_status['led2'] = 'OFF'
    return render_status()
 
def render_status():
    return render_template_string('''
        <h1>LED Status</h1>
        <p>LED 1 - {{ status_led1 }}</p>
        <p>LED 2 - {{ status_led2 }}</p>
        <h2>Control LEDs</h2>
        <p><a href="/led1/on">Turn LED 1 ON</a></p>
        <p><a href="/led1/off">Turn LED 1 OFF</a></p>
        <p><a href="/led2/on">Turn LED 2 ON</a></p>
        <p><a href="/led2/off">Turn LED 2 OFF</a></p>
    ''', status_led1=led_status['led1'], status_led2=led_status['led2'])
 
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
