using System;
using System.Drawing;
using System.Windows.Forms;

namespace CameraApp
{
    public partial class MainForm : Form
    {
        private PictureBox pictureBox;
        private Button startButton;
        private Button stopButton;
        private Timer timer;
        private VideoCapture capture;

        public MainForm()
        {
            InitializeComponent();
            InitializeCamera();
        }

        private void InitializeComponent()
        {
            this.pictureBox = new PictureBox();
            this.startButton = new Button();
            this.stopButton = new Button();
            this.SuspendLayout();
            // 
            // pictureBox
            // 
            this.pictureBox.Location = new Point(10, 10);
            this.pictureBox.Size = new Size(640, 480);
            this.pictureBox.BackColor = Color.Black;
            // 
            // startButton
            // 
            this.startButton.Location = new Point(10, 500);
            this.startButton.Size = new Size(75, 23);
            this.startButton.Text = "Start";
            this.startButton.Click += StartButton_Click;
            // 
            // stopButton
            // 
            this.stopButton.Location = new Point(100, 500);
            this.stopButton.Size = new Size(75, 23);
            this.stopButton.Text = "Stop";
            this.stopButton.Enabled = false;
            this.stopButton.Click += StopButton_Click;
            // 
            // MainForm
            // 
            this.ClientSize = new Size(660, 535);
            this.Controls.Add(this.pictureBox);
            this.Controls.Add(this.startButton);
            this.Controls.Add(this.stopButton);
            this.Text = "Camera App";
            this.ResumeLayout(false);
        }

        private void InitializeCamera()
        {
            capture = new VideoCapture();
            timer = new Timer();
            timer.Interval = 1000 / 30; // 30 frames per second
            timer.Tick += Timer_Tick;
        }

        private void Timer_Tick(object sender, EventArgs e)
        {
            if (capture.IsOpened())
            {
                Mat frame = capture.QueryFrame();
                if (frame != null)
                {
                    Bitmap bitmap = frame.ToBitmap();
                    pictureBox.Image = bitmap;
                }
            }
        }

        private void StartButton_Click(object sender, EventArgs e)
        {
            capture.Open(0); // Open the default camera (index 0)
            timer.Start();
            startButton.Enabled = false;
            stopButton.Enabled = true;
        }

        private void StopButton_Click(object sender, EventArgs e)
        {
            timer.Stop();
            capture.Release();
            startButton.Enabled = true;
            stopButton.Enabled = false;
        }
    }
}
