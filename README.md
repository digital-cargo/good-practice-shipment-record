<!--
---
title: shipment-tracking
repository: https://github.com/digital-cargo/good-practice-shipment-tracking
version: 1.0.0
maintainers: 
- Daniel A. Doeppner
- Ingo Zeschky
- Philipp Billion
ontologies:
- https://onerecord.iata.org/ns/cargo/3.0.0
- https://onerecord.iata.org/ns/api/2.0.0
- https://onerecord.iata.org/ns/coreCodeLists/0.0.3
data-classes:
- tbd
data-properties:
- tbd
api-version:
- 2.0.0
api-endpoints:
- method: GET 
  path: /logistics-objects/{logisticsObjectId} 
- method: GET 
  path: /logistics-objects/{logisticsObjectId}
- method: GET 
  path: /logistics-objects/{logisticsObjectId}/logistics-events
- method: GET 
  path: /logistics-objects/{logisticsObjectId}/logistics-events/{logisticsEventId}
- method: POST 
  path: /notifications
- method: GET 
  path: /subscriptions
- method: POST 
  path: /subscriptions
- method: GET 
  path: /action-requests/{actionRequestId} 
- method: DELETE
  path: /action-requests/{actionRequestId}
---
-->

# Good Practice: ShipmentTracking
[![Made with love for Digital Cargo](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%20for-Digital%20Cargo-dce435)](https://digital-cargo.org)
[![GitHub](https://img.shields.io/github/license/digital-cargo/good-practice-shipment-tracking)](https://creativecommons.org/licenses/by/4.0/)
[![Releases](https://img.shields.io/github/v/release/digital-cargo/good-practice-shipment-tracking)](https://github.com/digital-cargo/good-practice-shipment-tracking/releases)

## Abstract

tbd.

## Introduction

tbd

## Scope

tbd

## Data Mapping

	One Record datamodel, v3.0.0						Cargo XML - XFWB 3.0 xsd from IATA cXML Toolkit						
"DM3
RC5"	Object	Datafield type	Datafield, Datatype and Cardinality	Format / Validation rule	Description		XML Tags from cXML xsd	Message Example cXML					Comment / Required clarification / Mapping instruction
							<Êrsm:MessageHeaderDocumentÊ>	<ns2:MessageHeaderDocument>					
	see comment!						<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<ID>020-12345675</ID>				A: can be e.g. generated from AWB Prefix and Serial number
							<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>		<Name>Master Air Waybill</Name>				
	Waybill	Enum	type: enum	{ Direct , House , Master }	Type of the Waybill: House, Direct or Master		<Êram:TypeCodeÊ>XXXÊ</ram:TypeCode>		<TypeCode>741</TypeCode>				
							<Êram:IssueDateTimeÊ>2002-07-01T05:10:10Ê</ram:IssueDateTime>		<IssueDateTime>2023-02-24T10:23:50</IssueDateTime>				
	see comment!						<Êram:PurposeCodeÊ>XXXXXXXXXXÊ</ram:PurposeCode>		<PurposeCode>Update</PurposeCode>				A: can be set base on version of shipment record data, i.e. v1 => Creation; v2-n => Update
	see comment!						<Êram:VersionIDÊ>XXXXXXXXXXÊ</ram:VersionID>		<VersionID>3.00</VersionID>				A: Fixed value providing version number of cXML message
	see comment!			fix value			<Êram:ConversationIDÊ>XXXXXXXXXXÊ</ram:ConversationID>		<ConversationID>XYYZ45612348</ConversationID>				A: can be e.g. generated or taken over from 1R API
	IoL - Organization URI of Publisher/Delegator						Ê<Êram:SenderPartyÊ>		<SenderParty>				
	see comment!			t[...35]			<Êram:PrimaryIDÊschemeIDÊ="1"Ê>XXXXXXXXXXÊ</ram:PrimaryID>			<PrimaryID schemeID="P">REUAGT82XXX/YYY01</PrimaryID>			A: concept for transferring 1R Organization URI into PIMA Address to be defined / considered
							</ram:SenderParty>		</SenderParty>				
	IoL - Organization URI of Subscriber/User/Delegate						Ê<Êram:RecipientPartyÊ>		<RecipientParty>				
	see comment!			t[...35]			<Êram:PrimaryIDÊschemeIDÊ="1"Ê>XXXXXXXXXXÊ</ram:PrimaryID>			<PrimaryID schemeID="P">REUAIR08AAA</PrimaryID>			A: concept for transferring 1R Organization URI into PIMA Address to be defined / considered
							</ram:RecipientParty>		</RecipientParty>				
							</rsm:MessageHeaderDocument>	</ns2:MessageHeaderDocument>					
							Ê<rsm:BusinessHeaderDocument>	<ns2:BusinessHeaderDocument>					
	Carrier	Data	prefix: string		IATA three-numeric airline prefix number								I: used in Riege Converter i/o prefix from LO Waybill; in LO carrier no serial number is available
	Waybill	Data	prefix: string	nnn	Prefix used for the Waybill Number. Refer to IATA Airlines Codes		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<ID>020-12345675</ID>				
	Waybill	Data	waybillNumber: string	n[8]	House or Master Waybill unique identifier								A: in 1Rec separate elements for A/L Prefix and AWB Serial number
	Waybill	Data	optionalShippingRefNo: string		Optional shipping reference number if any		<Êram:SenderAssignedIDÊ>XXXXXXXXXXÊ</ram:SenderAssignedID>		<SenderAssignedID>A45645A6546</SenderAssignedID>				
							Ê<ram:IncludedHeaderNote>		<IncludedHeaderNote>				
	Waybill	Enum	waybillType: enum	{ Direct , House , Master }	Type of the Waybill: House, Direct or Master		<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>			<ContentCode>C</ContentCode>			
	see comment!						<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>			<Content>Consolidation</Content>			A: required for 1Rec / to be set during mapping, depending on type (AWB, HAWB, etc.)
							</ram:IncludedHeaderNote>		</IncludedHeaderNote>				
							Ê<ram:SignatoryConsignorAuthentication>		<SignatoryConsignorAuthentication>				
	Waybill	Data	consignorDeclarationSignature: string	t[...35]	Name of consignor signatory		<Êram:SignatoryÊ>XXXXXXXXXXÊ</ram:Signatory>			<Signatory>SHIPPER NAME</Signatory>			
							</ram:SignatoryConsignorAuthentication>		</SignatoryConsignorAuthentication>				
							Ê<ram:SignatoryCarrierAuthentication>		<SignatoryCarrierAuthentication>				
	Waybill	Data	carrierDeclarationDate: dateTime	yyyy-MM-DD[T]hhmm[Z]	Date upon which the certification is made by the carrier		<Êram:ActualDateTimeÊ>2002-07-01T05:10:10Ê</ram:ActualDateTime>			<ActualDateTime>2023-02-24T00:00:00</ActualDateTime>			A: 1R demands using UTC only, i.e. conversion into local time might be required during mapping
	Waybill	Data	carrierDeclarationSignature: string	t[É20]	Contains the authentication of the Carrier		<Êram:SignatoryÊ>XXXXXXXXXXÊ</ram:Signatory>			<Signatory>CARRIER OR AGENT NAME</Signatory>			
							Ê<ram:IssueAuthenticationLocation>			<IssueAuthenticationLocation>			
	Waybill	Object	carrierDeclarationPlace: Location: LocationCodes: code	CodeListElement	Location of individual or company involved in the movement of a consignment or Coded representation of a specific airport/city code		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>				<Name>DEMUC</Name>		
							</ram:IssueAuthenticationLocation>			</IssueAuthenticationLocation>			
							</ram:SignatoryCarrierAuthentication>		</SignatoryCarrierAuthentication>				
							</rsm:BusinessHeaderDocument>	</ns2:BusinessHeaderDocument>					
							Ê<rsm:MasterConsignment>	<ns2:MasterConsignment>					
							<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<FreightForwarderAssignedID>987654321</FreightForwarderAssignedID>				I: optional element not of any value for iCAP
							<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						I: optional element not of any value for iCAP
							<Êram:FreightForwarderAssignedIDÊ>XXXXXXXXXXÊ</ram:FreightForwarderAssignedID>						I: optional element not of any value for iCAP
							<Êram:AssociatedReferenceIDÊ>XXXXXXXXXXÊ</ram:AssociatedReferenceID>						I: optional element not of any value for iCAP
x	Waybill	Data	nvdForCarriage: boolean	true; false	When no value is declared for Carriage, this field may be completed with the value TRUE otherwise FALSE		<Êram:NilCarriageValueIndicatorÊ>trueÊ</ram:NilCarriageValueIndicator>		<NilCarriageValueIndicator>true</NilCarriageValueIndicator>				A: in 1Rec NVD (NIL) - ID is not available; to be generated during mapping if no value is available
x	Waybill	Data	declaredValueForCarriage:CurrencyValue:numericalValue	double			<Êram:DeclaredValueForCarriageAmountÊcurrencyIDÊ="XXX"Ê>XXXXXXXXXXÊ</ram:DeclaredValueForCarriageAmount>						
	Value	Data	CurrencyValue	CurrencyCode									
x	Waybill	Data	nvdForCustoms: boolean	true; false	When no value is declared for Customs, this field may be completed with the value TRUE otherwise FALSE		<Êram:NilCustomsValueIndicatorÊ>trueÊ</ram:NilCustomsValueIndicator>		<NilCustomsValueIndicator>true</NilCustomsValueIndicator>				A: in 1Rec NCV (NIL) - ID is not available; to be generated during mapping if no value is available
x	Waybill	Data	declaredValueForCustoms:CurrencyValue:numericalValue	double			<Êram:DeclaredValueForCustomsAmountÊcurrencyIDÊ="XXX"Ê>XXXXXXXXXXÊ</ram:DeclaredValueForCustomsAmount>						
	Value	Data	CurrencyValue	CurrencyCode									
	Insurance	Data	nvdIndicator: boolean	true; false	When no value is declared for Insurance this field should be completed with the value TRUE otherwise FALSE		<Êram:NilInsuranceValueIndicatorÊ>trueÊ</ram:NilInsuranceValueIndicator>		<NilInsuranceValueIndicator>true</NilInsuranceValueIndicator>				A: in 1Rec NIL - ID is not available; to be generated during mapping if no value is available
	Insurance	Object	insuredAmount:CurrencyValue:numericalValue	double	Insured amount - amount covered by the insurance policy		<Êram:InsuranceValueAmountÊcurrencyIDÊ="XXX"Ê>XXXXXXXXXXÊ</ram:InsuranceValueAmount>						
	Value	Data	CurrencyValue	CurrencyCode									
x	Waybill	Enum	weightValuationIndicator: enum	PrepaidCollectIndicator	payment for the Weight/Valuation will be made at origin (prepaid) or at destination (collect)		<Êram:TotalChargePrepaidIndicatorÊ>trueÊ</ram:TotalChargePrepaidIndicator>		<TotalChargePrepaidIndicator>true</TotalChargePrepaidIndicator>				
x	Waybill	Enum	otherChargesIndicator: enum	PrepaidCollectIndicator	payment of Other Charges will be made at origin (prepaid) or at destination (collect)		<Êram:TotalDisbursementPrepaidIndicatorÊ>trueÊ</ram:TotalDisbursementPrepaidIndicator>		<TotalDisbursementPrepaidIndicator>true</TotalDisbursementPrepaidIndicator>				
	Shipment	Object	totalGrossWeight:Value:numericalValue	double	Weight details		<Êram:IncludedTareGrossWeightMeasureÊunitCodeÊ="XXX"Ê>XXXXXXXXXXÊ</ram:IncludedTareGrossWeightMeasure>		<IncludedTareGrossWeightMeasure unitCode="KGM">3867.6</IncludedTareGrossWeightMeasure>				
x	see comment!												A: to be aggregated during mapping from weight provided on <Piece> level; if not available there to be mapped from <shipment> LO
	Value	Data	unit: MeasurementUnitCode	KGM	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
	Shipment	Data	Dimensions:volume:Value:numericalValue	double	Volume		<Êram:GrossVolumeMeasureÊunitCodeÊ="XXX"Ê>XXXXXXXXXXÊ</ram:GrossVolumeMeasure>		<GrossVolumeMeasure unitCode="MTQ">13.14</GrossVolumeMeasure>				A: Total shipment volume to be calculated from volumetric weight based on conversion factor during mapping
	Value	Data	unit: MeasurementUnitCode	MTQ	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
							<Êram:DensityGroupCodeÊ>XXXXXXXXXXÊ</ram:DensityGroupCode>						I: optional element not of any value for iCAP
x	Piece	Data	slac	integer	total slac from piece level, not related to ULD		<Êram:PackageQuantityÊ>XXXXXXXXXXÊ</ram:PackageQuantity>		<PackageQuantity>250</PackageQuantity>				"I: SLAC - independent value from ULD / Pallet / Container; separate datalement exists
A: During mapping total SLAC to be calculated from slac elements on piece level"
x	see comment!						<Êram:TotalPieceQuantityÊ>XXXXXXXXXXÊ</ram:TotalPieceQuantity>		<TotalPieceQuantity>87</TotalPieceQuantity>				A: in 1Rec no total piece count exists; to be derived from number of <Piece> LOs during mapping
							<Êram:ProductIDÊ>XXXXXXXXXXÊ</ram:ProductID>						I: optional element not of any value for iCAP
							Ê<ram:ConsignorParty>	<ConsignorParty>					
							<Êram:PrimaryIDÊschemeAgencyIDÊ="X"Ê>XXXXXXXXXXÊ</ram:PrimaryID>						
	Address	Data	addressCodeType: code	CodeListElement	Type of address code e.g. US CBP FIRMS		<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						
	Address	Data	addressCod: code	CodeListElement	Address identifier using special coding systems e.g. US CBP FIRMS code								A: not available in cXML; could be mapped into "Name" or "Address" tag of address !?
	Organization	Data	name: string	t[..70]	Name of the organization		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>		<Name>SHIPPER NAME</Name>				
	Party	Data	partyRole	ParticipantIdentifier	Role fo the Company in the context. Can refer to Code List 1.36 in the CXML Toolkit								A: to bet set during mapping if not available in source data
	Party	Data	otherIdentifiers (n): OtherIdentifier	enum	Reference to other identifiers for parties. In the context of the AWB, otherIdentifier object can be used with types "PrimaryID" (internal ID), "Additional ID" (Standard ID) or "AccountID" (Account numbers).		<Êram:AccountIDÊ>XXXXXXXXXXÊ</ram:AccountID>						
							Ê<ram:PostalStructuredAddress>		<PostalStructuredAddress>				
	Address	Data	postalCode: code	CodeListElement	Postal / ZIP code		<Êram:PostcodeCodeÊ>XXXXXXXXXXÊ</ram:PostcodeCode>			<PostcodeCode>85000</PostcodeCode>			
	Address	Data	streetAddressLines (n): string	t[..70]	Street address including street name, street number, building number, apartment etc		<Êram:StreetNameÊ>XXXXXXXXXXÊ</ram:StreetName>			<StreetName>SHIPPER STREET</StreetName>			
	Address	Data	cityName: string	t[..17]	Full name of the city		<Êram:CityNameÊ>XXXXXXXXXXÊ</ram:CityName>			<CityName>CITY NAME</CityName>			
	Address	Data	Country: code	CodeListElement	Country ISO code. Refer ISO 3166-2		<Êram:CountryIDÊ>XXXXXXXXXXÊ</ram:CountryID>			<CountryID>DE</CountryID>			
	Address	Data	Country: codeDescription	CodeListElement	Full country name, Refer ISO 3166-2		<Êram:CountryNameÊ>XXXXXXXXXXÊ</ram:CountryName>			<CountryName>GERMANY</CountryName>			
	Address	Data	regionName: codeDescription	CodeListElement	If no StateCode provided, full name of the region / state / province / canton		<Êram:CountrySubDivisionNameÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionName>						
	Address	Data	postBox: string		Post Office box number / code		<Êram:PostOfficeBoxÊ>XXXXXXXXXXÊ</ram:PostOfficeBox>						
	Address	Data	cityCode	CodeListElement	Standardized code of the city		<Êram:CityIDÊ>XXXXXXXXXXÊ</ram:CityID>						
	Address	Data	regionCode:code	CodeListElement	Region/ State / Department. Refer ISO 3166-2		<Êram:CountrySubDivisionIDÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionID>			<CountrySubDivisionID>BY</CountrySubDivisionID>			
							</ram:PostalStructuredAddress>		</PostalStructuredAddress>				
							Ê<ram:DefinedTradeContact>		<DefinedTradeContact>				
	Person	Data	firstName: string		First name / given name		<Êram:PersonNameÊ>XXXXXXXXXXÊ</ram:PersonName>						
	Person	Data	lastName: string		Last name / family name / surname								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	middleName: string		Middle name/ other name								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	department: string		Department / Division / Unit		<Êram:DepartmentNameÊ>XXXXXXXXXXÊ</ram:DepartmentName>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:DirectTelephoneCommunication>			<DirectTelephoneCommunication>			
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>				<CompleteNumber>49891234567</CompleteNumber>		
							</ram:DirectTelephoneCommunication>			</DirectTelephoneCommunication>			
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:FaxCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:FaxCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:URIEmailCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:URIIDÊ>XXXXXXXXXXÊ</ram:URIID>						
							</ram:URIEmailCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:TelexCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:TelexCommunication>						
							</ram:DefinedTradeContact>		</DefinedTradeContact>				
							</ram:ConsignorParty>	</ConsignorParty>					
							Ê<ram:ConsigneeParty>	<ConsigneeParty>					
							<Êram:PrimaryIDÊschemeAgencyIDÊ="1"Ê>XXXXXXXXXXÊ</ram:PrimaryID>						
	Address	Data	addressCodeType: code	CodeListElement	Type of address code e.g. US CBP FIRMS		<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						
	Address	Data	addressCod: code	CodeListElement	Address identifier using special coding systems e.g. US CBP FIRMS code								A: not available in cXML; could be mapped into "Name" or "Address" tag of address !?
	Organization	Data	name: string	t[..70]	Name of the organization		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>		<Name>CONSIGNEE NAME</Name>				
	Party	Data	partyRole	ParticipantIdentifier	Role fo the Company in the context. Can refer to Code List 1.36 in the CXML Toolkit								A: to bet set during mapping if not available in source data
	Party	Data	otherIdentifiers (n): OtherIdentifier	enum	Reference to other identifiers for parties. In the context of the AWB, otherIdentifier object can be used with types "PrimaryID" (internal ID), "Additional ID" (Standard ID) or "AccountID" (Account numbers).		<Êram:AccountIDÊ>XXXXXXXXXXÊ</ram:AccountID>						
							Ê<ram:PostalStructuredAddress>		<PostalStructuredAddress>				
	Address	Data	postalCode: code	CodeListElement	Postal / ZIP code		<Êram:PostcodeCodeÊ>XXXXXXXXXXÊ</ram:PostcodeCode>			<PostcodeCode>100015</PostcodeCode>			
	Address	Data	streetAddressLines (n): string	t[..70]	Street address including street name, street number, building number, apartment etc		<Êram:StreetNameÊ>XXXXXXXXXXÊ</ram:StreetName>			<StreetName>CONSIGNEE STREET </StreetName>			
	Address	Data	cityName: string	t[..17]	Full name of the city		<Êram:CityNameÊ>XXXXXXXXXXÊ</ram:CityName>			<CityName>BEIJING</CityName>			
	Address	Data	Country: code	CodeListElement	Country ISO code. Refer ISO 3166-2		<Êram:CountryIDÊ>CHÊ</ram:CountryID>			<CountryID>CN</CountryID>			
	Address	Data	Country: codeDescription	CodeListElement	Full country name, Refer ISO 3166-2		<Êram:CountryNameÊ>XXXXXXXXXXÊ</ram:CountryName>			<CountryName>CHINA</CountryName>			
	Address	Data	regionName: codeDescription	CodeListElement	If no StateCode provided, full name of the region / state / province / canton		<Êram:CountrySubDivisionNameÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionName>						
	Address	Data	postBox: string		Post Office box number / code		<Êram:PostOfficeBoxÊ>XXXXXXXXXXÊ</ram:PostOfficeBox>						
	Address	Data	cityCode	CodeListElement	Standardized code of the city		<Êram:CityIDÊ>XXXXXXXXXXÊ</ram:CityID>						
	Address	Data	regionCode:code	CodeListElement	Region/ State / Department. Refer ISO 3166-2		<Êram:CountrySubDivisionIDÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionID>						
							</ram:PostalStructuredAddress>		</PostalStructuredAddress>				
							Ê<ram:DefinedTradeContact>		<DefinedTradeContact>				
	Person	Data	firstName: string		First name / given name		<Êram:PersonNameÊ>XXXXXXXXXXÊ</ram:PersonName>						
	Person	Data	lastName: string		Last name / family name / surname								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	middleName: string		Middle name/ other name								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	department: string		Department / Division / Unit		<Êram:DepartmentNameÊ>XXXXXXXXXXÊ</ram:DepartmentName>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:DirectTelephoneCommunication>			<DirectTelephoneCommunication>			
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>				<CompleteNumber>008612346578</CompleteNumber>		
							</ram:DirectTelephoneCommunication>			</DirectTelephoneCommunication>			
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:FaxCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:FaxCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:URIEmailCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:URIIDÊ>XXXXXXXXXXÊ</ram:URIID>						
							</ram:URIEmailCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:TelexCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:TelexCommunication>						
							</ram:DefinedTradeContact>		</DefinedTradeContact>				
							</ram:ConsigneeParty>	</ConsigneeParty>					
							Ê<ram:FreightForwarderParty>						
							<Êram:PrimaryIDÊschemeAgencyIDÊ="X"Ê>XXXXXXXXXXÊ</ram:PrimaryID>		<FreightForwarderParty>				
	Address	Data	addressCodeType: code	CodeListElement	Type of address code e.g. US CBP FIRMS		<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						
	Address	Data	addressCod: code	CodeListElement	Address identifier using special coding systems e.g. US CBP FIRMS code								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Organization	Data	name: string	t[..70]	Name of the organization		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>			<Name>AGENT NAME</Name>			
	Party	Data	partyRole	ParticipantIdentifier	Role fo the Company in the context. Can refer to Code List 1.36 in the CXML Toolkit								A: to bet set during mapping if not available in source data
	Party	Data	otherIdentifiers (n): OtherIdentifier	enum	Reference to other identifiers for parties. In the context of the AWB, otherIdentifier object can be used with types "PrimaryID" (internal ID), "Additional ID" (Standard ID) or "AccountID" (Account numbers).		<Êram:AccountIDÊ>XXXXXXXXXXÊ</ram:AccountID>			<AccountID>1234FRA</AccountID>			
	Company	Data	iataCargoAgentCode: string	n[7]	IATA accredited cargo agent 7 digit number		<Êram:CargoAgentIDÊ>XXXXXXXXXXÊ</ram:CargoAgentID>			<CargoAgentID>2347041</CargoAgentID>			
							Ê<ram:FreightForwarderAddress>			<FreightForwarderAddress>			
	Address	Data	postalCode: code	CodeListElement	Postal / ZIP code		<Êram:PostcodeCodeÊ>XXXXXXXXXXÊ</ram:PostcodeCode>				<PostcodeCode>80000</PostcodeCode>		
	Address	Data	streetAddressLines (n): string	t[..70]	Street address including street name, street number, building number, apartment etc		<Êram:StreetNameÊ>XXXXXXXXXXÊ</ram:StreetName>				<StreetName>AGENT STREET</StreetName>		
	Address	Data	cityName: string	t[..17]	Full name of the city		<Êram:CityNameÊ>XXXXXXXXXXÊ</ram:CityName>				<CityName>AGENT CITY</CityName>		
	Address	Data	Country: code	CodeListElement	Country ISO code. Refer ISO 3166-2		<Êram:CountryIDÊ>CHÊ</ram:CountryID>				<CountryID>DE</CountryID>		
	Address	Data	Country: codeDescription	CodeListElement	Full country name, Refer ISO 3166-2		<Êram:CountryNameÊ>XXXXXXXXXXÊ</ram:CountryName>						
	Address	Data	regionName: codeDescription	CodeListElement	If no StateCode provided, full name of the region / state / province / canton		<Êram:CountrySubDivisionNameÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionName>						
	Address	Data	postBox: string		Post Office box number / code		<Êram:PostOfficeBoxÊ>XXXXXXXXXXÊ</ram:PostOfficeBox>						
	Address	Data	cityCode	CodeListElement	Standardized code of the city		<Êram:CityIDÊ>XXXXXXXXXXÊ</ram:CityID>						
	Address	Data	regionCode:code	CodeListElement	Region/ State / Department. Refer ISO 3166-2		<Êram:CountrySubDivisionIDÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionID>				<CountrySubDivisionID>BY</CountrySubDivisionID>		
							</ram:FreightForwarderAddress>			</FreightForwarderAddress>			
							Ê<ram:SpecifiedCargoAgentLocation>			<SpecifiedCargoAgentLocation>			
	Company	Data	iataCargoAgentLocationIdentifier: string	n[4]	IATA CASS cargo agent 4 digit branch number / location identifier		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>				<ID>8005</ID>		
							</ram:SpecifiedCargoAgentLocation>			</SpecifiedCargoAgentLocation>			
							Ê<ram:DefinedTradeContact>						
	Person	Data	firstName: string		First name / given name		<Êram:PersonNameÊ>XXXXXXXXXXÊ</ram:PersonName>						
	Person	Data	lastName: string		Last name / family name / surname								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	middleName: string		Middle name/ other name								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	department: string		Department / Division / Unit		<Êram:DepartmentNameÊ>XXXXXXXXXXÊ</ram:DepartmentName>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:DirectTelephoneCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:DirectTelephoneCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:FaxCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:FaxCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:URIEmailCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:URIIDÊ>XXXXXXXXXXÊ</ram:URIID>						
							</ram:URIEmailCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:TelexCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:TelexCommunication>						
							</ram:DefinedTradeContact>						
							</ram:FreightForwarderParty>		</FreightForwarderParty>				
							Ê<ram:AssociatedParty>						
							<Êram:PrimaryIDÊschemeAgencyIDÊ="X"Ê>XXXXXXXXXXÊ</ram:PrimaryID>						
	Address	Data	addressCodeType: code	CodeListElement	Type of address code e.g. US CBP FIRMS		<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						
	Address	Data	addressCod: code	CodeListElement	Address identifier using special coding systems e.g. US CBP FIRMS code								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Organization	Data	name: string	t[..70]	Name of the organization		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>						
	Party	Data	partyRole	ParticipantIdentifier	Role fo the Company in the context. Can refer to Code List 1.36 in the CXML Toolkit		<Êram:RoleCodeÊ>XXXXXXXXXXÊ</ram:RoleCode>						
							<Êram:RoleÊ>XXXXXXXXXXÊ</ram:Role>						
							Ê<ram:PostalStructuredAddress>						
	Address	Data	postalCode: code	CodeListElement	Postal / ZIP code		<Êram:PostcodeCodeÊ>XXXXXXXXXXÊ</ram:PostcodeCode>						
	Address	Data	streetAddressLines (n): string	t[..70]	Street address including street name, street number, building number, apartment etc		<Êram:StreetNameÊ>XXXXXXXXXXÊ</ram:StreetName>						
	Address	Data	cityName: string	t[..17]	Full name of the city		<Êram:CityNameÊ>XXXXXXXXXXÊ</ram:CityName>						
	Address	Data	Country: code	CodeListElement	Country ISO code. Refer ISO 3166-2		<Êram:CountryIDÊ>XXXXXXXXXXÊ</ram:CountryID>						
	Address	Data	Country: codeDescription	CodeListElement	Full country name, Refer ISO 3166-2		<Êram:CountryNameÊ>XXXXXXXXXXÊ</ram:CountryName>						
	Address	Data	regionName: codeDescription	CodeListElement	If no StateCode provided, full name of the region / state / province / canton		<Êram:CountrySubDivisionNameÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionName>						
	Address	Data	postBox: string		Post Office box number / code		<Êram:PostOfficeBoxÊ>XXXXXXXXXXÊ</ram:PostOfficeBox>						
	Address	Data	cityCode	CodeListElement	Standardized code of the city; Refer to UN/LOCODE or IATA city codes		<Êram:CityIDÊ>XXXXXXXXXXÊ</ram:CityID>						
	Address	Data	regionCode:code	CodeListElement	Region/ State / Department. Refer ISO 3166-2		<Êram:CountrySubDivisionIDÊ>XXXXXXXXXXÊ</ram:CountrySubDivisionID>						
							Ê<ram:SpecifiedAddressLocation>						
							<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						I: optional element not of any value for iCAP
							<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>						I: optional element not of any value for iCAP
							<Êram:TypeCodeÊ>XXXXXXXXXXÊ</ram:TypeCode>						I: optional element not of any value for iCAP
							</ram:SpecifiedAddressLocation>						
							</ram:PostalStructuredAddress>						
							Ê<ram:DefinedTradeContact>						
	Person	Data	firstName: string		First name / given name		<Êram:PersonNameÊ>XXXXXXXXXXÊ</ram:PersonName>						
	Person	Data	lastName: string		Last name / family name / surname								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	middleName: string		Middle name/ other name								A: in 1Rec separate elements exist for person info: to be considered during mapping
	Person	Data	department: string		Department / Division / Unit		<Êram:DepartmentNameÊ>XXXXXXXXXXÊ</ram:DepartmentName>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:DirectTelephoneCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:DirectTelephoneCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:FaxCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:FaxCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:URIEmailCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:URIIDÊ>XXXXXXXXXXÊ</ram:URIID>						
							</ram:URIEmailCommunication>						
	ContactDetail	Data	type	ContactDetailType or enum	Type of the contact details, e.g. Phone number, Mail address		Ê<ram:TelexCommunication>						
	ContactDetail	Data	textualValue: string	t[...25]	Value of the contact detail, e.g. phone number		<Êram:CompleteNumberÊ>XXXXXXXXXXÊ</ram:CompleteNumber>						
							</ram:TelexCommunication>						
							</ram:DefinedTradeContact>						
							</ram:AssociatedParty>						
							Ê<ram:OriginLocation>	<OriginLocation>					
	Waybill	Object	departureLocation: Location: LocationCodes: code	CodeListElement	Departure location details		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<ID>MUC</ID>				
							<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>		<Name>MUNICH</Name>				
							</ram:OriginLocation>	</OriginLocation>					
							Ê<ram:FinalDestinationLocation>	<FinalDestinationLocation>					
	Waybill	Object	arrivalLocation: Location: LocationCodes: code	CodeListElement	Arrival location details		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<ID>PEK</ID>				
							<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>		<Name>BEIJING CAPITAL</Name>				
							</ram:FinalDestinationLocation>	</FinalDestinationLocation>					
							Ê<ram:SpecifiedLogisticsTransportMovement>	<SpecifiedLogisticsTransportMovement>					
	TransportMovement	Enum	modeQualifier: enum	{ Main-Carriage , On-Carriage , Pre-Carriage }	Pre-Carriage, Main-Carriage or On-Carriage		<Êram:StageCodeÊ>XXXXXXXXXXÊ</ram:StageCode>		<StageCode>MAIN-CARRIAGE</StageCode>				I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
	TransportMovement	Data	modeCode: enum	{ "AirTransport, RoadTransport, etc."}	AirTransport, RoadTransport, etc.								
	TransportMovement	Data	transportIdentifier: string	mmnnn(n)(a)/nnaaannnn	Airline flight number, or rail /  truck / maritime line id		<Êram:ModeCodeÊ>XXXXXXXXXXÊ</ram:ModeCode>		<ID>LH7257</ID>				A: if available in cXML or other source data, to be mapped from here and departure Day/Month/Year to be added
							<Êram:ModeÊ>XXXXXXXXXXÊ</ram:Mode>						I: optional dataelement in cXML
							<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						
	see comment!						<Êram:SequenceNumericÊ>XXXXXXXXXXÊ</ram:SequenceNumeric>		<SequenceNumeric>1</SequenceNumeric>				A: not available; may be set during message generation; counter starting with 1 (optional dataelement in cXML)
							Ê<ram:UsedLogisticsTransportMeans>		<UsedLogisticsTransportMeans>				
	TransportMovement	Data	transportIdentifier: string	aa	Airline flight number, or rail /  truck / maritime line id		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>			<Name>LH</Name>			A: if only outing is available in cXML or other source data, CarrierCode to be used or derived from booking or other data source
							</ram:UsedLogisticsTransportMeans>		</UsedLogisticsTransportMeans>				
							Ê<ram:ArrivalEvent>		<ArrivalEvent>				A: Arrival time information to be mapped into planned arrival time
	TransportMovement	Object	LogisticsEvent: eventTimeType	{ACTUAL, ESTIMATED, PLANNED}									A: to be set to PLANNED
	TransportMovement	Object	LogisticsEvent: eventDate: dateTime	yyyy-MM-DD[T]hhmm[Z]	Link to events describing the arrival		<Êram:ScheduledOccurrenceDateTimeÊ>2002-07-01T05:10:10Ê</ram:ScheduledOccurrenceDateTime>						"I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
A: 1R demands using UTC only, i.e. conversion into local time might be required during mapping"
							Ê<ram:OccurrenceArrivalLocation>			<OccurrenceArrivalLocation>			
	TransportMovement	Object	arrivalLocation: Location: LocationCodes: code	CodeListElement	Arrival location details		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>				<ID>FRA</ID>		
	see comment!						<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>						A: not available; can be set during message generation, default "AIRPORT"
							<Êram:TypeCodeÊ>XXXXXXXXXXÊ</ram:TypeCode>				<TypeCode>AIRPORT</TypeCode>		I: optional dataelement in cXML
							</ram:OccurrenceArrivalLocation>			</OccurrenceArrivalLocation>			
							</ram:ArrivalEvent>		</ArrivalEvent>				
							Ê<ram:DepartureEvent>		<DepartureEvent>				A: Departure time information to be mapped into planned departure time
	TransportMovement	Object	LogisticsEvent: eventTimeType	{ACTUAL, ESTIMATED, PLANNED}									A: to be set to PLANNED
	TransportMovement	Object	LogisticsEvent: eventDate: dateTime	yyyy-MM-DD[T]hhmm[Z]	Links to events describing the depature		<Êram:ScheduledOccurrenceDateTimeÊ>2002-07-01T05:10:10Ê</ram:ScheduledOccurrenceDateTime>			<ScheduledOccurrenceDateTime>2023-02-25T21:00:00</ScheduledOccurrenceDateTime>			A: 1R demands using UTC only, i.e. conversion into local time might be required during mapping
							Ê<ram:OccurrenceDepartureLocation>						
	TransportMovement	Object	departureLocation: Location: LocationCodes: code	CodeListElement	Departure location details		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
							<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
							<Êram:TypeCodeÊ>XXXXXXXXXXÊ</ram:TypeCode>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
							</ram:OccurrenceDepartureLocation>						
							</ram:DepartureEvent>		</DepartureEvent>				
							</ram:SpecifiedLogisticsTransportMovement>	</SpecifiedLogisticsTransportMovement>					
							Ê<ram:UtilizedLogisticsTransportEquipment>						
	TransportMeans	Data	vehicleRegistration: string		Vehicle identification - e.g. aircraft registration number		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
	TransportMeans	Data	vehicleType: code	CodeListElement	Vehicle or container type. Refer UNECE28, e.g. 4.00.0 - Aircraft, type unknown.For Air refer to IATA Standard Schedules Information Manua in section ATA/IATA Aircraft Types		<Êram:CharacteristicCodeÊ>XXXXXXXXXXÊ</ram:CharacteristicCode>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
	TransportMeans	Data	vehicleSize: string		Size of the vehicle - free text		<Êram:CharacteristicÊ>XXXXXXXXXXÊ</ram:Characteristic>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
							Ê<ram:AffixedLogisticsSeal>						
	TransportMovement	Data	seal: string		Seal identifier		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						I: optional dataelement in cXML; can be mapped for information purpose but no impact on processing of data
							</ram:AffixedLogisticsSeal>						
							</ram:UtilizedLogisticsTransportEquipment>						
	see comment!						Ê<ram:HandlingSPHInstructions>	<HandlingSPHInstructions>					A: mapped from separate LO <specialHandlingCodes> on piece level; i.e. to be aggregated on shipment level
							<Êram:DescriptionÊ>XXXXXXXXXXÊ</ram:Description>						A: Non IATA SPL Codes not to be mapped if included; SPL Codes now available, both on Shipment and Piece level
x	Shipment	Data	specialHandlingCodes	SpecialHandlingCode	Service Type code linked top the Service Type. Refers to Code List 1.14 or 1.16 if service type is Special Handling.		<Êram:DescriptionCodeÊ>XXXXXXXXXXÊ</ram:DescriptionCode>		<DescriptionCode>EAP</DescriptionCode>				
	Piece	Data	specialHandlingCodes	SpecialHandlingCode									A: If provided on Piece level: to mapped from separate LO <specialHandlingCodes> on piece level; i.e. to be aggregated on shipment level
	SecurityDeclaration	Data	securityStatus	SecurityStatus									A: If SCC Code is a Security status such as SPX, SHR, SCO or NSC, to ne mapped into SecurityStatus
							</ram:HandlingSPHInstructions>	</HandlingSPHInstructions>					
							Ê<ram:HandlingSSRInstructions>	<HandlingSSRInstructions>					
x	Shipment	Data	textualHandlingInstructions: string	t[É250]	Free text description of the handling instructions		<Êram:DescriptionÊ>XXXXXXXXXXÊ</ram:Description>		<Description>+++MULTIMASTER WITH 020-12345678+++</Description>				A: in 1R Handling Info text can be provided on Piece or Shipment level; if provided on piece level, aggregation is required during mapping
	see comment!						<Êram:DescriptionCodeÊ>XXXXXXXXXXÊ</ram:DescriptionCode>						A: text to be spread over SSR and OSI during mapping in order to prevent exceeding max. characters
							</ram:HandlingSSRInstructions>	</HandlingSSRInstructions>					
							Ê<ram:HandlingOSIInstructions>	<HandlingOSIInstructions>					
x	Shipment	Data	textualHandlingInstructions: string	t[É250]	Free text description of the handling instructions		<Êram:DescriptionÊ>XXXXXXXXXXÊ</ram:Description>	       <Description>ENCL MARKED ADDRESS DOCS ATTACHED TO AIRWAYBILL</Description>					A: in 1R Handling Info text can be provided on Piece or Shipment level; if provided on piece level, aggregation is required during mapping
	see comment!						<Êram:DescriptionCodeÊ>XXXXXXXXXXÊ</ram:DescriptionCode>						A: text to be spread over SSR and OSI during mapping in order to prevent exceeding max. characters
							</ram:HandlingOSIInstructions>	     </HandlingOSIInstructions>					
							Ê<ram:IncludedAccountingNote>	<IncludedAccountingNote>					
	see comment!						<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>GEN</ContentCode>				A: not available; must be set during message generation, e.g. GEN as default
	Waybill	Data	accountingInformation: string	t[É250]	Indicates the details of accounting information. Free text e.g. PAYMENT BY CERTIFIED CHEQUE etc.		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>LH,TDP</Content>				
							</ram:IncludedAccountingNote>	</IncludedAccountingNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
x	CustomsInformation	Data	contentCode: code	CodeListElement	Customs, Security and Regulatory Control Information Identifier. Coded indicator qualifying Customs related information: Item Number "I", Exemption Legend "L", System Downtime Reference "S", Unique Consignment Reference Number "U", Movement Reference Number "M" . Refers to Code List 1.100 Condition: At least one of the three elements (Country Code, Information Identifier or Customs, Security and Regulatory Control Information Identifier) must be completed		<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>T</ContentCode>				
x	CustomsInformation	Data	otherCustomsInformation: string	t[É35]	Supplementary Customs, Security and Regulatory Control Information		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>EUROPEAN VAT NUMBERDE64654645</Content>				
x	CustomsInformation	Data	subjectCode: code	CodeListElement	Information Identifier. Code identifying a piece of information/entity e.g. "IMP" for import, "EXP" for export, "AGT" for Agent, "ISS" for The Regulated Agent Issuing the Security Status for a Consignment etc.  Condition: At least one of the three elements (Country Code, Information Identifier or Customs, Security and Regulatory Control Information Identifier) must be completed		<Êram:SubjectCodeÊ>XXXXXXXXXXÊ</ram:SubjectCode>		<SubjectCode>SHP</SubjectCode>				
x	CustomsInformation	Data	country: code	CodeListElement	Customs country code. Refer ISO 3166-2 Condition:  At least one of the three elements (Country Code, Information Identifier or Customs, Security and Regulatory Control Information Identifier) must be completed		<Êram:CountryIDÊ>XXXXXXXXXXÊ</ram:CountryID>		<CountryID>DE</CountryID>				
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
	SecurityDeclaration	Data	regulatedEntityIssuer:RegulatedEntity	regulatedEntityCategoryCode	e.g. RA, KC etc.		<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>RA</ContentCode>				A: RegulatedEntityIssuer to be mapped to/from details associated with SubjectCode ISS - Issuing Party
		Data	regulatedEntityIssuer:RegulatedEntity	regulatedEntityIdentifier	Identification number		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>00181-08</Content>				
	see comment!						<Êram:SubjectCodeÊ>XXXXXXXXXXÊ</ram:SubjectCode>	         <SubjectCode>ISS</SubjectCode>					I: In 1R no separate data element exists for subject code; to be derived from RegulatedEntity type; here ISS
							<Êram:CountryIDÊ>XXXXXXXXXXÊ</ram:CountryID>	         <CountryID>DE</CountryID>					
		Data	regulatedEntityIssuer:RegulatedEntity:owningOrganization	Organization: Name	Name of party owning information								A: In 1R this dataelement can be used to indicate party who owns the provided information; in cXML no equivalent element exists
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
	SecurityDeclaration	Data	receivedFrom:RegulatedEntity	regulatedEntityCategoryCode	e.g. RA, KC etc.		<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>KC</ContentCode>				A: received From party relates to e.g. cases SPX by KC or SPX by RA; in cXML no SubjectCode is used
		Data	receivedFrom:RegulatedEntity	regulatedEntityIdentifier	Identification number		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>00192-10</Content>				
		Data	receivedFrom:RegulatedEntity:owningOrganization	Organization: Name	Name of party owning information								A: In 1R this dataelement can be used to indicate party who owns the provided information; in cXML no equivalent element exists
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
	SecurityDeclaration	Data	RegulatedAcceptor:RegulatedEntity	regulatedEntityCategoryCode	e.g. RA, KC etc.		<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>RA</ContentCode>				A: RegulatedEntityAcceptor to be mapped to/from details associated with SubjectCode OSS - Accepting Party
		Data	RegulatedAcceptor:regulatedEntity	regulatedEntityIdentifier	Identification number		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>00015-01</Content>				
	see comment!						<Êram:SubjectCodeÊ>XXXXXXXXXXÊ</ram:SubjectCode>	               <SubjectCode>OSS</SubjectCode>					I: In 1R no separate data element exists for subject code; to be derived from RegulatedEntity type; here ISS
		Data	RegulatedAcceptor:RegulatedEntity:owningOrganization	Organization: Name	Name of party owning information								A: In 1R this dataelement can be used to indicate party who owns the provided information; in cXML no equivalent element exists
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
	see comment!						<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>SN</ContentCode>				A: ContentCode not available in 1R; i.e. to be generated during mapping
	SecurityDeclaration	Data	issuedBy: Person: firstName & lastName	t[É35]	Issued By information		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>Sebastian Koebel</Content>				
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:IncludedCustomsNote>	<IncludedCustomsNote>					
	see comment!						<Êram:ContentCodeÊ>XXXXXXXXXXÊ</ram:ContentCode>		<ContentCode>SD</ContentCode>				A: ContentCode not available in 1R; i.e. to be generated during mapping
	SecurityDeclaration	Data	issuedOn: dateTime	yyyy-MM-DD[T]hhmm[Z]	Issued On information		<Êram:ContentÊ>XXXXXXXXXXÊ</ram:Content>		<Content>18Jan231000</Content>				A: conversion from UTC into local time required as part of mapping
							</ram:IncludedCustomsNote>	</IncludedCustomsNote>					
							Ê<ram:AssociatedReferenceDocument>						
	ExternalReference	Data	id	string	Unique document identifier		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						
	ExternalReference	Data	validFrom	string			<Êram:IssueDateTimeÊ>2002-07-01T05:10:10Ê</ram:IssueDateTime>						A: In cXML only issue date exists; might be taken over from LO validFrom and/or generated during mapping; UTC time zone to be used
	ExternalReference	Data	type	string	Type of the referenced document . Can refer UNEDIFACT 1001  e.g. 740 - Air Waybill, but not limited to		<Êram:TypeCodeÊ>XXXXXXXXXXÊ</ram:TypeCode>						
	ExternalReference	Data	name	string	If no DocumentType provided, name of the referenced document		<Êram:NameÊ>XXXXXXXXXXÊ</ram:Name>						
							</ram:AssociatedReferenceDocument>						
							Ê<ram:AssociatedConsignmentCustomsProcedure>	<AssociatedConsignmentCustomsProcedure>					
	Waybill	Data	customsOriginCode: string	m[É2]	Code indicating the origin of goods for Customs purposes (e.g. For goods in free circulation in the EU)  List to be provided by local authorities		<Êram:GoodsStatusCodeÊ>XXXXXXXXXXÊ</ram:GoodsStatusCode>		<GoodsStatusCode>X</GoodsStatusCode>				
							</ram:AssociatedConsignmentCustomsProcedure>	</AssociatedConsignmentCustomsProcedure>					
							Ê<ram:ApplicableOriginCurrencyExchange>	<ApplicableOriginCurrencyExchange>					
	see comment!		mapping removed				<Êram:SourceCurrencyCodeÊ>CHFÊ</ram:SourceCurrencyCode>		<SourceCurrencyCode>EUR</SourceCurrencyCode>				A: For Currency Codes in 1R no dedicated dataelements exist; handled via CodeLists separately for each monetary amount field
							</ram:ApplicableOriginCurrencyExchange>	</ApplicableOriginCurrencyExchange>					
							Ê<ram:ApplicableDestinationCurrencyExchange>						
	see comment!		mapping removed				<Êram:TargetCurrencyCodeÊ>XXXÊ</ram:TargetCurrencyCode>						A: For Currency Codes in 1R no dedicated dataelements exist; handled via CodeLists separately for each monetary amount field
							<Êram:MarketIDÊ>XXXXXXXXXXÊ</ram:MarketID>						I: optional element not of any value for iCAP
	Waybill	Data	destinationCurrencyRate	double	Conversion rate applied		<Êram:ConversionRateÊ>XXXXXXXXXXÊ</ram:ConversionRate>						
							</ram:ApplicableDestinationCurrencyExchange>						
							Ê<ram:ApplicableLogisticsServiceCharge>						
	Waybill	Data	carrierChargeCode	ChargeCode			<Êram:TransportPaymentMethodCodeÊ>XXXXXXXXXXÊ</ram:TransportPaymentMethodCode>						
	Waybill	Data	serviceCode	ServiceCode	Service Type code linked top the Service Type. Refers to Code List 1.14 or 1.16 if service type is Special Handling.		<Êram:ServiceTypeCodeÊ>XXXXXXXXXXÊ</ram:ServiceTypeCode>						
							</ram:ApplicableLogisticsServiceCharge>						
							Ê<ram:ApplicableLogisticsAllowanceCharge>	<ApplicableLogisticsAllowanceCharge>					
x	otherCharge	string	otherchargecode	OtherChargeCode			<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>		<ID>MY</ID>				
							<Êram:AdditionalIDÊ>XXXXXXXXXXÊ</ram:AdditionalID>						I: optional element not of any value for iCAP
x	otherCharge	string	chargePaymentType	PrepaidCollectIndicator			<Êram:PrepaidIndicatorÊ>trueÊ</ram:PrepaidIndicator>		<PrepaidIndicator>true</PrepaidIndicator>				A: during mapping: P = true; C = false
							<Êram:LocationTypeCodeÊ>OÊ</ram:LocationTypeCode>						I: optional element not of any value for iCAP
							<Êram:ReasonÊ>XXXXXXXXXXÊ</ram:Reason>						I: optional element not of any value for iCAP
x	otherCharge	string	entitlement	EntitlementCode			<Êram:PartyTypeCodeÊ>XXXXXXXXXXÊ</ram:PartyTypeCode>		<PartyTypeCode>C</PartyTypeCode>				
x	otherCharge	value	otherChargeAmount:Value:CurrencyValue:numericalValue	double	Other charge amount		<Êram:ActualAmountÊcurrencyIDÊ="XXX"Ê>XXXXXXXXXXÊ</ram:ActualAmount>		<ActualAmount currencyID="EUR">4061.4</ActualAmount>				
x	Value	Data	CurrencyValue: currencyUnit	CurrencyCode	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
							<Êram:TimeBasisQuantityÊ>23Ê</ram:TimeBasisQuantity>						I: optional element not of any value for iCAP
							<Êram:ItemBasisQuantityÊ>23Ê</ram:ItemBasisQuantity>						I: optional element not of any value for iCAP
							<Êram:ServiceDateÊ>2002-07-01T05:10:10Ê</ram:ServiceDate>						I: optional element not of any value for iCAP
							<Êram:SpecialServiceDescriptionÊ>XXXXXXXXXXÊ</ram:SpecialServiceDescription>						I: optional element not of any value for iCAP
							<Êram:SpecialServiceTimeÊ>2002-07-01T05:10:10Ê</ram:SpecialServiceTime>						I: optional element not of any value for iCAP
							</ram:ApplicableLogisticsAllowanceCharge>	</ApplicableLogisticsAllowanceCharge>					
							Ê<Êram:ApplicableRatingÊ>	<ApplicableRating>					
	see comment!						<Êram:TypeCodeÊ>FÊ</ram:TypeCode>		<TypeCode>F</TypeCode>				A: to be set to "F" during mapping
x	see comment!						<Êram:TotalChargeAmountÊcurrencyIDÊ="USD"Ê>23Ê</ram:TotalChargeAmount>		<TotalChargeAmount currencyID="EUR">14002.16</TotalChargeAmount>				A: to be calculated from sum of weight charges, i.e. values from waybillLineItem <total> values
													I: note: in cXML this data element is redundant / identical with total weight charges provided in <ApplicableTotalRating>
							<Êram:ConsignmentItemQuantityÊ>23Ê</ram:ConsignmentItemQuantity>						I: optional element not of any value for iCAP; can be used to map number of RTD lines included in message
							Ê<ram:IncludedMasterConsignmentItem>		<IncludedMasterConsignmentItem>				
	waybillLineItems	Data	lineItemNumber	integer			<Êram:SequenceNumericÊ>23Ê</ram:SequenceNumeric>			<SequenceNumeric>1</SequenceNumeric>			
	waybillLineItems	Data	hsCodeForRate	CodeListElement	Harmonized Commodity code, refer to hsType used. 6 minimum digits are expected.		<Êram:TypeCodeÊlistAgencyIDÊ="1"Ê>XXXXXXXXXXÊ</ram:TypeCode>			<TypeCode listAgencyName="EU Harmonized System Code">85044095</TypeCode>			
x	waybillLineItems	Data	grossWeightForRate: Value: numericalValue	double			<Êram:GrossWeightMeasureÊunitCodeÊ="KGM"Ê>23Ê</ram:GrossWeightMeasure>		<GrossWeightMeasure unitCode="KGM">3867.6</GrossWeightMeasure>				I: related to TACT RateDescription information
x	Value	Data	unit: MeasurementUnitCode	KGM	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
x	waybillLineItems	Data	Dimensions: Volume: Value: numericalValue	double	Volume to weight conversion factor		<Êram:GrossVolumeMeasureÊunitCodeÊ="CBM"Ê>23Ê</ram:GrossVolumeMeasure>		<GrossVolumeMeasure unitCode="MTQ">13.14</GrossVolumeMeasure>				
	see comment!												A: RTD volume to be calculated from TACT chargeable weight value based on conversion factor during mapping
x	Value	Data	unit: MeasurementUnitCode	MTQ	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
x	waybillLineItems	Data	slacForRate	integer	Shipper's Load And Count  ( total contained piece count as provided by shipper)		<Êram:PackageQuantityÊ>23Ê</ram:PackageQuantity>		<PackageQuantity>255</PackageQuantity>				I: SLAC fŸr ULD can be provided either in new data element added to waybillLineItems or as part of class Loading Unit
x	waybillLineItems	Data	pieceCountForRate	integer			<Êram:PieceQuantityÊ>23Ê</ram:PieceQuantity>		<PieceQuantity>87</PieceQuantity>				I: related to TACT RateDescription information
							<Êram:VolumetricFactorÊ>XXXXXXXXXXÊ</ram:VolumetricFactor>						I: optional element not of any value for iCAP
	see comment!						<Êram:InformationÊ>XXXXXXXXXXÊ</ram:Information>		<Information>NDA</Information>				A: to be set to NDA during mapping if no dimensions are available
							Ê<ram:NatureIdentificationTransportCargo>		<NatureIdentificationTransportCargo>				
	Piece	Data	goodsDescription: string	t[É250]	General goods description		<Êram:IdentificationÊ>XXXXXXXXXXÊ</ram:Identification>			<Identification>CONSOLIDATION AS PER ATTACHED MANIFEST>			"A: GoodsDescription also added to waybillLineItems with RC6; to be considered during mapping;
     possibly to be mapped twice, once for Piece, once for Waybill"
	waybillLineItems	Data	goodsDescription	string	General goods description								
	see comment!						</ram:NatureIdentificationTransportCargo>		</NatureIdentificationTransportCargo>				A: in 1R goodsDescription is available, both on shipment and on piece level; if piece level is used, aggregation is required during mapping
							Ê<ram:OriginCountry>						
	waybillLineItems	Data	productionCountryForRate: code	CodeListElement			</ram:OriginCountry>						A: production country now also added to waybillLineItems; during mapping both positions should be considered
							Ê<ram:AssociatedUnitLoadTransportEquipment>		<AssociatedUnitLoadTransportEquipment>				A: physical ULD information provieded her must be linked to UldRateDetails from waybill class if applicable
	waybillLineItems	Data	uldSerialNumber: string	mnnn(n)	ULD serial number		<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>			<ID>88836</ID>			
	waybillLineItems	Object	uldTareWeightForRate: Value: numericalValue	double	Tare weight of the empty ULD		<Êram:TareWeightMeasureÊunitCodeÊ="KGM"Ê>23Ê</ram:TareWeightMeasure>						
	Value	Data	unit: MeasurementUnitCode	KGM	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
x	waybillLineItems	Data	slacForRate	integer	Shipper's Load And Count  ( total contained piece count as provided by shipper)		<Êram:LoadedPackageQuantityÊ>23Ê</ram:LoadedPackageQuantity>			<LoadedPackageQuantity>120</LoadedPackageQuantity>			I: SLAC also in 1R available at two places, once ULD, once non-ULD related; see also above
	waybillLineItems	Data	uldType: code	CodeListElement	Standard Unit Load Device type code e.g. AKE - Certified Container - Contoured. Refer to IATA ULD Technical Manual		<Êram:CharacteristicCodeÊ>XXXXXXXXXXÊ</ram:CharacteristicCode>			<CharacteristicCode>PMC</CharacteristicCode>			
							Ê<ram:OperatingParty>			<OperatingParty>			
	waybillLineItems	Data	uldOwnerCode: code	CodeListElement	Owner code of the ULD in aa, an or na format - owner can be an airline or leasing company		<Êram:PrimaryIDÊschemeAgencyIDÊ="1"Ê>XXXXXXXXXXÊ</ram:PrimaryID>				<PrimaryID schemeAgencyID="1">LH</PrimaryID>		
							</ram:OperatingParty>			</OperatingParty>			
							</ram:AssociatedUnitLoadTransportEquipment>		</AssociatedUnitLoadTransportEquipment>				
							Ê<ram:TransportLogisticsPackage>		<TransportLogisticsPackage>				I: For RateDescription level information separate LOs are planned to be added to datamodel as part of RC5
x	see comment!				Quantity of the item when applicable, with associated units of measure		<Êram:ItemQuantityÊ>23Ê</ram:ItemQuantity>		<ItemQuantity>1</ItemQuantity>				A: Piece count for dimnension item to be aggregated during mapping from <Piece> LOs with same dimensions
x	Value	Data	grossWeight: value: numericalValue	double	Weight of the item		<Êram:GrossWeightMeasureÊunitCodeÊ="KGM"Ê>23Ê</ram:GrossWeightMeasure>						A: Gross Weight value for dimnension item to be aggregated during mapping from <Piece> LOs with same dimensions
	Value	Data	unit: MeasurementUnitCode	KGM	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
							Ê<ram:LinearSpatialDimension>		  <LinearSpatialDimension>				
	Dimensions	Object	height: Value: numericalValue	double	Width		<Êram:WidthMeasureÊunitCodeÊ="CMT"Ê>23Ê</ram:WidthMeasure>		<WidthMeasure unitCode="CMT">90</WidthMeasure>				
	Value	Data	unit: MeasurementUnitCode	CMT	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
	Dimensions	Object	height: Value: numericalValue	double	Length		<Êram:LengthMeasureÊunitCodeÊ="CMT"Ê>23Ê</ram:LengthMeasure>		<LengthMeasure unitCode="CMT">140</LengthMeasure>				
	Value	Data	unit: MeasurementUnitCode	CMT	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
	Dimensions	Object	height: Value: numericalValue	double	Height		<Êram:HeightMeasureÊunitCodeÊ="CMT"Ê>23Ê</ram:HeightMeasure>		<HeightMeasure unitCode="CMT">95</HeightMeasure>				
	Value	Data	unit: MeasurementUnitCode	CMT	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
							</ram:LinearSpatialDimension>		  </LinearSpatialDimension>				
							</ram:TransportLogisticsPackage>		</TransportLogisticsPackage>				
							Ê<ram:ApplicableFreightRateServiceCharge>		<ApplicableFreightRateServiceCharge>				
x	waybillLineItems	Data	rateClassCode	RateClassCode			<Êram:CategoryCodeÊ>XXXXXXXXXXÊ</ram:CategoryCode>			<CategoryCode>Q</CategoryCode>			
x	waybillLineItems	Data	commodityItemNumberForRate: string	string			<Êram:CommodityItemIDÊ>XXXXXXXXXXÊ</ram:CommodityItemID>						
x	waybillLineItems	Data	chargeableWeightForRate:Value: numericalValue	double	Chargeable weight		<Êram:ChargeableWeightMeasureÊunitCodeÊ="KGM"Ê>23Ê</ram:ChargeableWeightMeasure>			<ChargeableWeightMeasure unitCode="KGM">3868</ChargeableWeightMeasure>			
x	Value	Data	unit: MeasurementUnitCode	KGM	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
x	waybillLineItems	Data	rateCharge: Value: numericalValue	double			<Êram:AppliedRateÊ>23Ê</ram:AppliedRate>			<AppliedRate>3.62</AppliedRate>			I: amount from LO Ranges used
	Value	Data	CurrencyValue: currencyUnit	CurrencyCode									
x	waybillLineItems	Data	total: Value: numericalValue	double			<Êram:AppliedAmountÊcurrencyIDÊ="USD"Ê>23Ê</ram:AppliedAmount>			<AppliedAmount currencyID="EUR">14002.16</AppliedAmount>			I: in 1R Shipmenr Record to be included together with chargeType "FREIGHT"
x	Value	Data	CurrencyValue: currencyUnit	CurrencyCode	Unit of measurement/ unit of account e.g. CMT - Centimetre,  LTR - Litre (1 DM3), KGM - Kilogram, CHF - Swiss Franc								A: in 1Rec separate elements for unit and value; to be considered during mapping
							</ram:ApplicableFreightRateServiceCharge>		</ApplicableFreightRateServiceCharge>				
													
x	waybillLineItems	Data	rcp: Location: locationCodes: code	CodeListElement			<Êram:IDÊ>XXXXXXXXXXÊ</ram:ID>						
							Ê<ram:ApplicableUnitLoadDeviceRateClass>						
x	waybillLineItems	Data	uldRateClassType	CodeListElement			<Êram:TypeCodeÊ>XXXXXXXXXXÊ</ram:TypeCode>						
x	waybillLineItems	Data	rateClassCodeBasis	BasicRateClassCode			<Êram:BasisCodeÊ>XXXXXXXXXXÊ</ram:BasisCode>						
x	waybillLineItems	Data	ratePercentage: Value: numericalValue	double			<Êram:AppliedPercentÊ>23Ê</ram:AppliedPercent>						
	Value	Data	unit: MeasurementUnitCode	P1	P1: Percent								
							</ram:IncludedMasterConsignmentItem>	</IncludedMasterConsignmentItem>					
							</ram:ApplicableRating>	</ApplicableRating>					
							Ê<Êram:ApplicableTotalRatingÊ>	<ApplicableTotalRating>					
	see comment!						<Êram:TypeCodeÊ>FÊ</ram:TypeCode>		<TypeCode>F</TypeCode>				A: not available; must be set during message generation; default should be "F"
	see comment!						Ê<ram:ApplicablePrepaidCollectMonetarySummation>		<ApplicablePrepaidCollectMonetarySummation>				A: As part of mapping all total amounts must be calculated from individual amounts provided in related data elements
x	see comment!						<Êram:PrepaidIndicatorÊ>trueÊ</ram:PrepaidIndicator>			<PrepaidIndicator>true</PrepaidIndicator>			A: during mapping to be set: IF "P" then true, else false
x	see comment!						<Êram:WeightChargeTotalAmountÊcurrencyIDÊ="USD"Ê>23Ê</ram:WeightChargeTotalAmount>			<WeightChargeTotalAmount currencyID="EUR">14002.16</WeightChargeTotalAmount>			A: to be calculated from sum of weight charges, i.e. sum of <total> values from waybillLineItems, separated by payment type
x	see comment!						<Êram:CarrierTotalDuePayableAmountÊcurrencyIDÊ="USD"Ê>23Ê</ram:CarrierTotalDuePayableAmount>			<CarrierTotalDuePayableAmount currencyID="EUR">4074.4</CarrierTotalDuePayableAmount>			A: to be calculated from otherChargeAmount values from OtherCharge class, separated by payment type and entitlement
x	see comment!						<Êram:GrandTotalAmountÊcurrencyIDÊ="USD"Ê>23Ê</ram:GrandTotalAmount>			<GrandTotalAmount currencyID="EUR">18076.56</GrandTotalAmount>			A: to be calculated from sum of all prepaid and/or collect charges, separated by payment type
							</ram:ApplicablePrepaidCollectMonetarySummation>		</ApplicablePrepaidCollectMonetarySummation>				
							</ram:ApplicableTotalRating>		</ApplicableTotalRating>				
							</rsm:MasterConsignment>		</ns2:MasterConsignment>				
							</rsm:Waybill>	</ns2:Waybill>					
													
													

## Glossary
see [digita-cargo/glossary](https://github.com/digital-cargo/glossary)

## References

- ...
- ...
- ...
  
## Acknowledgements

The initial version of this document is the outcome of the 
"Joint ONE Record piloting and transition working group // technical part" at IATA. 
It was orchestrated by Arnaud Lambert of IATA as secretary and [Philipp Billion](https://github.com/DrPhilippBillion) of Lufthansa Cargo as chairman.

Special thanks to [Niclas Scheiber](https://github.com/NiclasScheiber), Frankfurt University of Applied Sciences for preparing version 3.0.0 of the 
ONE Record core ontology in coordination with the IATA ONE Record data model focus group.

## Community

### Contribute

See [CONTRIBUTING](CONTRIBUTING.md) for more details on how to contribute on this good practice.

### Issues
Issues related to this good practice are tracked on GitHub

- [View open issues](https://github.com/digital-cargo/good-practice-shipment-tracking/issues)
- [Create a new issue](https://github.com/digital-cargo/good-practice-shipment-tracking/issues/new)

### Maintainers

> Each good practice MUST have at least one maintainer who is responsible for ongoing development and quality assurance. 
> Every maintainer MUST have commit access to the good practice repository.

- [Daniel A. Döppner](https://github.com/ddoeppner), Lufthansa Industry Solutions 
- [Ingo Zeschky](https://github.com/ChrisKranich), Lufthansa Cargo
- [Philipp Billion](https://github.com/DrPhilippBillion), Lufthansa Cargo

_(sorted alphabetically)_

### Contributors

> Every good practice is the result of the work of the community, and therefore the contribution of each individual should be recognized and appreciated. 
> Below is a list of all the people who have actively contributed to this good practice.

- Ajay Manoharan, Qatar Airways
- Arnaud Lambert, IATA
- Bilel Chakroun, Air France-KLM 
- Josh Priebe, Air Canada
- Keith Lam, GLS HKG 
- Mark Belliss, British Telecom 
- Martin Fowler, MDF Solutions
- [Martin Skopp](https://github.com/mskopp), Riege Software
- Mary Stradling, DHL
- Matthias Hurst, Colog AG
- Pramod Rao, Nexshore Technologies
- [Ying Lu](https://github.com/luyinglu), Lufthansa Cargo

_(sorted alphabetically)_


