# stevieb0000.github.io
Gym testing project
{
  "name": "ironpeak-gym",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "axios": "^1.5.0",
    "next": "13.5.1",
    "react": "18.2.0",
    "react-dom": "18.2.0"
  }
}
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true
}

module.exports = nextConfig;
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-color: #111;
  color: #fff;
}

a {
  color: #ff4500;
  text-decoration: none;
}

button {
  background-color: #ff4500;
  color: #fff;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}
import Link from 'next/link';

export default function Navbar(){
  return (
    <nav style={{display:'flex', justifyContent:'space-between', padding:'20px', background:'#222'}}>
      <div><Link href="/">IronPeak</Link></div>
      <div style={{display:'flex', gap:'20px'}}>
        <Link href="/">Home</Link>
        <Link href="/about">About</Link>
        <Link href="/programs">Programs</Link>
        <Link href="/membership">Membership</Link>
        <Link href="/contact">Contact</Link>
      </div>
    </nav>
  )
}
export default function Footer(){
  return (
    <footer style={{background:'#222', color:'#fff', textAlign:'center', padding:'20px', marginTop:'50px'}}>
      <p>© 2025 IronPeak Strength Gym</p>
      <div>Follow us: Instagram | Facebook | TikTok</div>
    </footer>
  )
}
export default function Hero(){
  return (
    <div style={{textAlign:'center', padding:'100px 20px', background:'#111'}}>
      <h1 style={{fontSize:'48px'}}>Unlock Your Strength. Lift Heavy. Transform Your Body.</h1>
      <p style={{fontSize:'20px', margin:'20px 0'}}>Elite coaching, world-class equipment, and a supportive community built for lifters of all levels.</p>
      <button style={{marginRight:'10px'}}>Join the Gym</button>
      <button>Book a Free Intro Session</button>
    </div>
  )
}
export default function ProgramCard({ title, description }) {
  return (
    <div style={{border:'1px solid #444', padding:'20px', borderRadius:'10px', margin:'10px', flex:'1'}}>
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  )
}
import Navbar from '../components/Navbar';
import Footer from '../components/Footer';
import Hero from '../components/Hero';

export default function Home() {
  return (
    <>
      <Navbar />
      <Hero />
      <div className="container">
        <h2>Welcome to IronPeak Strength Gym</h2>
        <p>Your premier facility for weight-lifting, powerlifting, and strength training. Train smarter, lift heavier, achieve your peak performance.</p>
      </div>
      <Footer />
    </>
  )
}
import Navbar from '../components/Navbar';
import Footer from '../components/Footer';

export default function About(){
  return (
    <>
      <Navbar />
      <div className="container">
        <h1>About IronPeak Strength Gym</h1>
        <p>IronPeak Strength Gym is a performance-focused facility for lifters of all levels, offering expert coaching, competition-grade equipment, and a community dedicated to strength.</p>
      </div>
      <Footer />
    </>
  )
}
import Navbar from '../components/Navbar';
import Footer from '../components/Footer';
import ProgramCard from '../components/ProgramCard';

export default function Programs(){
  const programs = [
    {title:'IronStarter', description:'Beginner program teaching fundamentals and safe technique.'},
    {title:'PeakPower', description:'Powerlifting specialization for squat, bench, deadlift.'},
    {title:'MassBuilder', description:'Hypertrophy program for muscle growth.'},
    {title:'Athlete Pro', description:'Performance program for speed, power, explosiveness.'}
  ];

  return (
    <>
      <Navbar />
      <div className="container">
        <h1>Programs</h1>
        <div style={{display:'flex', flexWrap:'wrap'}}>
          {programs.map((p,i)=><ProgramCard key={i} {...p} />)}
        </div>
      </div>
      <Footer />
    </>
  )
}
import Navbar from '../components/Navbar';
import Footer from '../components/Footer';

export default function Membership(){
  const plans = [
    {title:'Standard', price:'$39/mo', features:['24/7 access','Full gym use']},
    {title:'Pro Lifter', price:'$69/mo', features:['Everything in Standard','Weekly coaching','Monthly check-in']},
    {title:'Elite Coaching', price:'$149/mo', features:['Personalized program','Weekly 1-on-1 coaching','Full analytics dashboard']}
  ];

  return (
    <>
      <Navbar />
      <div className="container">
        <h1>Membership Plans</h1>
        <div style={{display:'flex', gap:'20px', flexWrap:'wrap'}}>
          {plans.map((plan,i)=>(
            <div key={i} style={{border:'1px solid #444', padding:'20px', borderRadius:'10px', flex:'1'}}>
              <h2>{plan.title}</h2>
              <h3>{plan.price}</h3>
              <ul>{plan.features.map((f,j)=><li key={j}>{f}</li>)}</ul>
              <button>Join Now</button>
            </div>
          ))}
        </div>
      </div>
      <Footer />
    </>
  )
}
import Navbar from '../components/Navbar';
import Footer from '../components/Footer';
import { useState } from 'react';
import axios from 'axios';

export default function Contact() {
  const [form, setForm] = useState({ name: '', email: '', phone: '', message: '' });
  const [success, setSuccess] = useState('');

  const handleChange = (e) => setForm({ ...form, [e.target.name]: e.target.value });

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const res = await axios.post('/api/contact', form);
      setSuccess(res.data.message);
      setForm({ name: '', email: '', phone: '', message: '' });
    } catch (err) {
      setSuccess('Error submitting form.');
    }
  };

  return (
    <>
      <Navbar />
      <div className="container">
        <h1>Contact Us</h1>
        {success && <p>{success}</p>}
        <form onSubmit={handleSubmit} style={{ display: 'flex', flexDirection: 'column', gap: '10px', maxWidth:'500px'}}>
          <input name="name" value={form.name} onChange={handleChange} placeholder="Name" required />
          <input name="email" value={form.email} onChange={handleChange} placeholder="Email" required />
          <input name="phone" value={form.phone} onChange={handleChange} placeholder="Phone" />
          <textarea name="message" value={form.message} onChange={handleChange} placeholder="Message" required />
          <button type="submit">Send Message</button>
        </form>
      </div>
      <Footer />
    </>
  );
}
import fs from 'fs';
import path from 'path';

export default function handler(req, res) {
  if (req.method === 'POST') {
    const { name, email, phone, message } = req.body;

    if (!name || !email || !message) {
      return res.status(400).json({ error: 'Please fill all required fields.' });
    }

    const dbPath = path.join(process.cwd(), 'contacts.json');

    let db = { contacts: [] };
    if (fs.existsSync(dbPath)) {
      db = JSON.parse(fs.readFileSync(dbPath, 'utf8'));
    }

    db.contacts.push({ name, email, phone, message, date: new Date() });
    fs.writeFileSync(dbPath, JSON.stringify(db, null, 2));

    res.status(200).json({ message: 'Contact submitted successfully.' });
  } else {
    res.status(405).json({ error: 'Method not allowed' });
  }
}
