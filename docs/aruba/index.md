---
layout: default
title: Aruba Guide
has_children: true
nav_exclude: true
---

# Aruba IoT Configuration Guide

This document describes the principals and configuration of the Aruba IoT integrations using ArubaOS/Aruba Instant version 8.8.0.0 or higher.

### **Table of contents**

*  [Aruba IoT concepts](#aruba-iot-concepts)  
  
    *  [IoT connectivity (radio-side)](#iot-connectivity-radio-side)  

       *  [Wi-Fi](#wi-fi)
       *  [Aruba IoT radio](#aruba-iot-radio)
       *  [USB/3rd party IoT radio's](#usb3rd-party-iot-radios)  

    *  [IoT server connectivity (server-side)](#iot-server-connectivity-server-side)  
  
       *  [Aruba IoT server interface](#aruba-iot-server-interface)
          *  [Server connection types](#server-connection-types)
             *  [Telemetry-Https](#telemetry-https)
             *  [Telemetry-Websocket](#telemetry-websocket)
             *  [Azure-IoTHub](#azure-iothub)
          *  [Server connection encryption](#server-connection-encryption)
          *  [Authentication and authorization](#authentication-and-authorization)
          *  [Connection management](#connection-management)

       *  [IoT transport services](#iot-transport-services)
          *  [Wi-Fi telemetry](#wi-fi-telemetry)
          *  [Wi-Fi RTLS data forwarding](#wi-fi-rtls-data-forwarding)
          *  [BLE telemetry](#ble-telemetry)
          *  [BLE data forwarding](#ble-data-forwarding)
          *  [BLE connect](#ble-connect)
          *  [Serial-data](#serial-data)
          *  [ZigBee socket device](#zigbee-socket-device)

       *  [Device class filter](#device-class-filter)  
          *  [BLE device class filter](#ble-device-class-filter)  
       *  [Data contet filters](#data-content-filters)  
          *  [General data filter](#general-data-filter)
          *  [BLE data filter](#ble-data-filter)

*  [Configuration](#configuration)  
  
   *  [IoT radio profile](#iot-radio-profile)
   *  [IoT transport profile](#iot-transport-profile)
   *  [AP USB device management](#ap-usb-device-management)
   *  [Wired-Port profile](#wired-port-profile)
   *  [SES Imagotag ESL configuration](#ses-imagotag-esl-configuration) 
   *  [ZigBee configuration](#zigbee-configuration) 

*  [Configuration examples](#configuration-examples)  
  
   *  [IoT-Utilities App](#iot-utilities-app)
      *  [IoT-Utilities App (ArubaOS/Aruba Instant 8.7.x.x)](#iot-utilities-app-arubaosaruba-instant-87xx)
      *  [IoT-Utilities App (ArubaOS/Aruba Instant 8.8.x.x or higher)](#iot-utilities-app-arubaosaruba-instant-88xx-or-higher)
   *  [Wi-Fi solutions](#wi-fi-solutions)  
      *  [Wi-Fi client tracking solution](#wi-fi-client-tracking-solution)
      *  [Wi-Fi RTLS data forwarding solution](#wi-fi-rtls-data-forwarding-solution)
   *  [BLE vendor specific solutions](#ble-vendor-specific-solutions)  
      *  [Aruba Meridian Beacon Management](#aruba-meridian-beacon-management)
      *  [Aruba Meridian Asset Tracking](#aruba-meridian-asset-tracking)
      *  [ZF Openmatics](#zf-openmatics)
   *  [BLE telemetry solutions](#ble-telemetry-solutions)
      *  [iBeacon + Eddystone asset tracking](#ibeacon--eddystone-asset-tracking)
      *  [HYPROS (ArubaOS/Aruba Instant 8.7.x.x)](#hypros-arubaosaruba-instant-87xx)
      *  [HYPROS (ArubaOS/Aruba Instant 8.8.x.x or higher)](#hypros-arubaosaruba-instant-88xx-or-higher)
   *  [BLE data forwarding solutions](#ble-data-forwarding-solutions)
      *  [Azure IoT Hub (ble data)](#azure-iot-hub-ble-data)
   *  [BLE connect solutions](#ble-connect-solutions)
      *  [ABB (ArubaOS/Aruba Instant 8.7.x.x)](#abb-arubaosaruba-instant-87xx)
      *  [ABB (ArubaOS/Aruba Instant 8.8.x.x or higher)](#abb-arubaosaruba-instant-88xx-or-higher)
   *  [USB vendor specific solutions](#usb-vendor-specific-solutions)
      *  [SES Imagotag](#ses-imagotag)
   *  [USB-to-ethernet solutions](#usb-to-ethernet-solutions)
      *  [Solu-M ESL](#solu-m-esl)
   *  [USB-to-serial solutions](#usb-to-serial-solutions)
      *  [EnOcean demo](#enocean-demo)
      *  [Azure IoT Hub (serial-data)](#azure-iot-hub-serial-data)
   *  [Zigbee solutions](#zigbee-solutions)
      *  [ASSA ABLOY](#assa-abloy)
      *  [Generic ZSD solution](#generic-zsd-solution)
  
*  [Appendix](#appendix)  

    *  [Aruba reference documenation](#aruba-reference-documentation)
    *  [Aruba IoT server interface - connection types](#aruba-iot-server-interface---connection-types)
    *  [Supported IoT vendor/device class list](#supported-iot-vendordevice-class-list)
    *  [Supported USB vendor list for IoT](#supported-usb-vendor-list-for-iot)  